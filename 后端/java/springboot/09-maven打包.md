## 1 确认 maven 插件

首先你要确定你是否在 `spring boot` 项目中使用了 `maven` 插件

```xml
<plugin>  
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-maven-plugin</artifactId>  
    <version>${spring-boot.version}</version>  
    <configuration>        <mainClass>xyz.bibiyes.study.StudyApplication</mainClass>  
        <skip>false</skip>  
    </configuration>    <executions>        <execution>            <id>repackage</id>  
            <goals>                <goal>repackage</goal>  
            </goals>        </execution>    </executions></plugin>
```
