# 控制器
`Spring boot` 提供了 `@Controller` 和 `RestController` 两种注解来**标识此类负责接受和处理**HTTP 请求
## 1. `@controller`
一个普通控制器返回的是一个**视图**就是一个 html 页面
`Controller` 通常与 `Thymeleaf` 模板引擎结合使用
**示例代码**
```java

```

## 2. `@RestController`
这个注解会将返回的**对象**数据转换为 `json` 格式
```java
```
### 2.1. 路由映射
`@RequestMapping` 注解主要负责 URL 的路由映射。它可以添加在 `Controller` 类或者具体的**方法上面**
>如果添加到了 `Controller` 类上，则这个 `Controller` 中的所有的路由映射都会加上此映射规则，如果添加在方法上则只对当前方法生效

**添加在方法上**
![[Pasted image 20240319192942.png]]
## 3. 携参请求
这分别是 `get请求` 和 `post` 请求的取参数示例
```java
@GetMapping("/getTest1")  
public String hello(String nickname,String phone) {  
    System.out.println(phone);  
    return "你好"+ nickname;  
}  
@PostMapping("/postTest1")  
public String postTest1(String nickname, String password){  
    System.out.println(nickname+password);  
    return "POST请求";  
}
```
> 直接在**方法**内写接受的变量就行了

### 3.1. 携参请求对象
前端发送大量数据的时候会使用**对象的形式**发送到后台我们又是如何去接受这个对象呢？
1. 首先我们需要先**创建一个类**这类就可以抽离出一个对象用来存储**前端发来的对象**
```java
package org.mouse.charpper01.enity;  
  
public class User {  
    private String nickname;  
    private String password;  
    // 规定了传递过来对象的类型
  
    public String getNickname() {  
        return nickname;  
    }  
  
    public void setNickname(String nickname) {  
        this.nickname = nickname;  
    }  
  
    public String getPassword() {  
        return password;  
    }  
  
    public void setPassword(String password) {  
        this.password = password;  
    }  
  
    @Override  
    public String toString() {  
        return "User{" +  
                "nickname='" + nickname + '\'' +  
                ", password='" + password + '\'' +  
                '}';  
    }  
}
```
> 一个基本的类有 get 和 set 方法

2. 将接受到的**前端对象**存储到 **java 对象中**
```java
@PostMapping("/postTest2")  
public String postTest1(User user){  
    System.out.println(user);  
    return "POST请求";  
}
```
**什么？如果你说前端发送过来的是 json 格式呢？**
```java
@PostMapping("/postTest3")  
public String postTest3(@RequestBody User user){  
    System.out.println(user);  
    return "POST请求";  
}
```
> 使用 `@RequestBody` 注解