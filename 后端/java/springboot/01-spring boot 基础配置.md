#配置
## 1. 全局配置文件

在 `spring boot` 项目根目录下有一个这样的文件 `application.properties`
我们可以在这里书写对 `spring boot` 项目的配置

[这里在线文档有关于`application.properties`的所有配置](https://docs.spring.io/spring-boot/appendix/application-properties/index.html#appendix.application-properties.server)

## 2. 一些常见的配置信息

1. **`tomcat` 服务器端口配置**

```yaml
server:
# 将服务器端口设置为8080
  port: 8080
```

2. **虚拟目录设置**

```yaml

```

## 3. 外部配置文件

Spring Boot 支持将外部配置文件（`application.properties` 或 `application.yml`）放置在应用的外部路径中，来覆盖 JAR 文件内部的配置。优先级顺序是外部配置文件优先于内部配置文件。
部署时，将一个自定义的配置文件（如 `application.properties` 或 `application.yml`）放置在 JAR 文件的外部。
例如，假设你的应用程序打包成了 `study.jar`，你可以创建一个外部的 `application.properties` 文件并将其放置在如下路径：
![[Pasted image 20240923162144.png]]
输入一下命令启动 `jar` 包，并且启用外部配置文件

```shell
java -jar .\study-0.0.1-SNAPSHOT.jar --spring.config.location=file:./application.yaml
```

## 4. yaml 配置信息书写与获取

在 Spring Boot 项目中，我们通常会使用自定义配置，并且可以通过外部配置文件（例如 `application.properties` 或 `application.yml`）来管理这些配置。这样，即使在项目打包后，我们也能方便地修改配置，而无需重新构建或打包应用。例如，以下是我们定义的一个自定义配置项

```yaml
# 自定义配置文件
email:
  user: luozihao
  code: 12345678
  host: smtp.qq.com
  auth: true
```
我们可以通过 `@Value` 来获取配置文件的值
比如我们在实体类中
```java
package xyz.bibiyes.study.entity;  
import org.springframework.stereotype.Component;  
import lombok.AllArgsConstructor;  
import lombok.Data;  
import lombok.NoArgsConstructor;  
import lombok.ToString;  
import org.springframework.beans.factory.annotation.Value;  
@Data  
@AllArgsConstructor  
@NoArgsConstructor  
@ToString  
@Component  // 让 Spring 管理这个类  
public class User {  
    @Value("${email.user}")  // 正确的配置键  
    private String name;  
  
    @Value("${email.code}")  // 确保这里也匹配配置文件  
    private int code;  
  
    @Value("${email.host}")  // 同上  
    private String host;  
  
    @Value("${email.auth}")  // 确保类型匹配，这里看起来应该是 boolean    private boolean auth;  
}
```
这些私有的变量优先会采用配置文件中的值

### 4.1. 简化写法
使用  `@ConfigurationProperties(prefix = "email")` 来达到简化写法
它可以根据**前缀**和**变量名**自动装配符合的参数的属性
**示例**
```java
@ConfigurationProperties(prefix = "email")  
public class User {  
	// 根据前缀 email 和 变量名 得出 email.user
    private String user;  
  

    private int code;  
  

    private String host;  
  
 
}
```
> [!warning] 注意 
> 
> 一定要添加这个@Component，否则spring 不会扫描到这个bean
