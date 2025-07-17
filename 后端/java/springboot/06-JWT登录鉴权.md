#java #springboot
在用户登陆后，后台会给前台发送一个凭证（token），前台请求的时候需要带上这个凭证，才可以访问接口
## 1. WebMvc 拦截器
使用 WebMvc 指定统一的接口前缀
```java
import org.springframework.context.annotation.Configuration;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.servlet.config.annotation.PathMatchConfigurer;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;
@Configuration
public class Webconfig implements WebMvcConfigurer {
    @Override
    public void configurePathMatch(PathMatchConfigurer configurer) {
        //指定controller统一的接口前缀
        configurer.addPathPrefix("/api", clazz -> clazz.isAnnotationPresent(RestController.class));
    }
}
```
## 2. JWT 的规则
1. 首先你需要先导入 `Jwt` 包
```xml
<dependency>  
    <groupId>com.auth0</groupId>  
    <artifactId>java-jwt</artifactId>  
    <version>3.10.3</version>  
</dependency>
```
2. 创建一个名为 `JwtTokenUtil` 的类用来生成 ` Token `
```java
import cn.hutool.core.date.DateUtil;  
import com.auth0.jwt.JWT;  
import com.auth0.jwt.algorithms.Algorithm;  
import org.springframework.stereotype.Component;  
import java.util.Date;  
@Component  
public class JwtTokenUtils {  
   public static String genToken(String userId, String password) {  
        System.out.println("正在生成token");  
        return JWT.create().withAudience(userId)
                .withExpiresAt(DateUtil.offsetHour(new Date(), 2)) 
                .sign(Algorithm.HMAC256(password)); 
    }  
}
```
> 可以在登录`service`中调用此方法生成`token`，返回给用户
3. 随后**前端**前端就把**后端**返回来的token装载在*请求头*中
```js
// 添加请求拦截器
request.interceptors.request.use(
  function (config) {
    // 获取localStorage 存储的用户数据 user
    const user = localStorage.getItem('user')
    // 如果能取到的 就将用数据中的token字段添加到请求头里去
    if (user) {
      config.headers['token'] = JSON.parse(user).token
      console.log(JSON.parse(user).token);
    }
    // 在发送请求之前做些什么
    return config
  },
  function (error) {
    // 对请求错误做些什么
    return Promise.reject(error)
  }
)
```
> 在请求拦截器中添加配置
4. 前端已经在**请求头**中添加了`token`，随后我需要书写一个拦截配置 新建一个拦截器配置`JwtInterceptor`
```java
import cn.hutool.core.util.StrUtil;  
import com.auth0.jwt.JWT;  
import com.auth0.jwt.JWTVerifier;  
import com.auth0.jwt.algorithms.Algorithm;  
import com.auth0.jwt.exceptions.JWTVerificationException;  
import com.example.springboot.entity.Admin;  
import com.example.springboot.exception.CustomException;  
import com.example.springboot.service.AdminService;  
import org.slf4j.Logger;  
import org.slf4j.LoggerFactory;  
import org.springframework.stereotype.Component;  
import org.springframework.web.servlet.HandlerInterceptor;  
import javax.annotation.Resource;  
import javax.servlet.http.HttpServletRequest;  
import javax.servlet.http.HttpServletResponse;  
/**  
 * jwt拦截器  
 */  
@Component  
public class JwtInterceptor implements HandlerInterceptor {  
    private static final Logger log = LoggerFactory.getLogger(JwtInterceptor.class);  
    @Resource  
    private AdminService adminService;  
    @Override  
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) {  
        // 1. 从http请求的header中获取token  
        String token = request.getHeader("Token");  
        System.out.println(token);  
        if (StrUtil.isBlank(token)) {  
            // 如果没拿到，我再去参数里面拿一波试试  /api/admin?token=xxxxx            token = request.getParameter("token");  
        }  
        // 2. 开始执行认证  
        if (StrUtil.isBlank(token)) {  
            throw new CustomException("无token，请重新登录");  
        }  
        // 获取 token 中的userId  
        String userId;  
        Admin admin;  
        try {  
            userId = JWT.decode(token).getAudience().get(0);  
            // 根据token中的userid查询数据库  
            admin = adminService.findByById(Integer.parseInt(userId));  
        } catch (Exception e) {  
            String errMsg = "token验证失败，请重新登录";  
            log.error("{}, token={}", errMsg, token, e);  
            throw new CustomException(errMsg);  
        }  
        if (admin == null) {  
            throw new CustomException("用户不存在，请重新登录");  
        }  
        try {  
            // 用户密码加签验证 token            JWTVerifier jwtVerifier = JWT.require(Algorithm.HMAC256(admin.getPassword())).build();  
            jwtVerifier.verify(token); // 验证token  
        } catch (JWTVerificationException e) {  
            throw new CustomException("token验证失败，请重新登录");  
        }  
        System.out.println("验证成功");  
        return true;  
    }  
}
```
5. 拦截器配置已经写好了接下来我们需要，将这个配置添加到`Spring MVC`里
```java
import org.springframework.context.annotation.Configuration;  
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;  
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;  
import javax.annotation.Resource;  
// 标注这是一个配置类  
@Configuration  
public class WebConfig implements WebMvcConfigurer {  
    @Resource  
    private JwtInterceptor jwtInterceptor;  
    // 加自定义拦截器JwtInterceptor，设置拦截规则  
    @Override  
    public void addInterceptors(InterceptorRegistry registry) {  
        // 添加拦截的路径  
        registry.addInterceptor(jwtInterceptor).addPathPatterns("/api/**")  
                // 设置不拦截的路径  
                .excludePathPatterns("/api/login")  
                .excludePathPatterns("/api/register");  
    }  
}
```

## 3. 跨域问题
如果你遇到 跨域问题 试着书写以下类
```java
import org.springframework.context.annotation.Bean;  
import org.springframework.context.annotation.Configuration;  
import org.springframework.web.cors.CorsConfiguration;  
import org.springframework.web.cors.UrlBasedCorsConfigurationSource;  
import org.springframework.web.filter.CorsFilter;  
  
@Configuration  
public class CorsConfig {  
  
    @Bean  
    public CorsFilter corsFilter() {  
        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();  
        CorsConfiguration corsConfiguration = new CorsConfiguration();  
        corsConfiguration.addAllowedOrigin("*"); // 1 设置访问源地址  
        corsConfiguration.addAllowedHeader("*"); // 2 设置访问源请求头  
        corsConfiguration.addAllowedMethod("*"); // 3 设置访问源请求方法  
        source.registerCorsConfiguration("/**", corsConfiguration); // 4 对接口配置跨域设置  
        return new CorsFilter(source);  
    }
```