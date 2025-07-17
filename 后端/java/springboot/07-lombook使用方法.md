
## 1. 在实体中使用
> 使用这些注解可以快速生成方法
```java
 
import lombok.ToString;  
import lombok.Data;
import lombok.NoArgsConstructor;  
import lombok.AllArgsConstructor;

// 生成get set方法
@Data  
@ToString  
// 生成无参构造方法
@NoArgsConstructor  
// 生成全参构造方法
@AllArgsConstructor  
public class Questions {  
    private int id;  
    private String title;  
    private String content;  
    private String prompt;  
    private String uploadDate;  
}
```
