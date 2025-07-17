## 1. bean 注册
如何注册第三方bean?
在 `springboot ` 注册一个我们自己的类直接使用 `@conponent` 注解即可直接注册
首先我们需要先创建一个**配置类**，该配置类专门用来注册三方 `bean`
1. 创建一个 `config` 包
2. 创建一个 `commonConfig` 类 如下
```java
// 将该类标记为配置类 让springboot 扫描到  
@Configuration  
public class commonConfig {  
    @Bean  
    public User user(){  
        return new User();  
    }  
}
```
**我们来解释一下这个两个注解**
* `@Configuration` 将该类标记为**配置类**被 `spring` 管理
* `BeanBean` 返回值将被注册为 `Spring` 容器中的一个 `Bean`，这意味着该对象会被 ` Spring 管理 `，可以被依赖注入（DI）机制使用。
我们看看你注册的这个 `bean` 是都能在 ` springboot ` 上下文中找到
```java
@SpringBootApplication  
public class StudyApplication {  
  
    public static void main(String[] args) {  
        ConfigurableApplicationContext context  =  SpringApplication.run(StudyApplication.class, args);  
        User user = context.getBean(User.class);  
        System.out.println(user);  
    }   
}
```
我们得到的结果是
![[Pasted image 20240924113759.png]]
## 2. 注册条件
可以在注册传递一些参数
![[Pasted image 20240924124222.png]]
## 3. 自动配置原理
遵循约定大于配置的原则，在 `boot` 程序启动后，启动依赖中的一些 `bean` 对象会自动注入到 ioc 容器 `