## 1. java RESTful 返回模板
* 每一个 URL 代表一种层次感
* 资源的表现形式是 JSON 或者HTML
**返回状态码**

**通用的 `RESTAPI`** 模板
```java  
import java.util.List;
import java.util.Map;

public class Result {

    private int code;
    private String type;
    private String msg;
	private List<Map<String, Object>> data;

    // Constructor
    public Result() {}

    public Result(int code, String type, String msg, List<Map<String, Object>> data) {
        this.code = code;
        this.type = type;
        this.msg = msg;
        this.data = data;
    }

    // Getters and Setters
    public int getCode() {
        return code;
    }

    public void setCode(int code) {
        this.code = code;
    }

    public String getType() {
        return type;
    }

    public void setType(String type) {
        this.type = type;
    }

    public String getMsg() {
        return msg;
    }

    public void setMsg(String msg) {
        this.msg = msg;
    }

    public List<Map<String, Object>> getData() {
        return data;
    }

    public void setData(List<Map<String, Object>> data) {
        this.data = data;
    }

    // Static methods for success and failure
    public static Result success(String type, String msg, List<Map<String, Object>> data) {
        Result result = new Result();
        result.setCode(200);
        result.setType(type);
        result.setMsg(msg);
        result.setData(data);
        return result;
    }

    public static Result failure(int code, String type, String msg) {
        Result result = new Result();
        result.setCode(code);
        result.setType(type);
        result.setMsg(msg);
        result.setData(null);
        return result;
    }

    @Override
    public String toString() {
        return "Result{" +
                "code=" + code +
                ", type='" + type + '\'' +
                ", msg='" + msg + '\'' +
                ", data=" + data +
                '}';
    }
}

```

## 2. 如何设计遵循 `RESTful` 规范的接口 

接口请求路径（API URL）通常遵循 **RESTful** 风格，这是最常见和推荐的接口设计方式之一。RESTful API 通过 **资源**（resource）和 **动作**（action）的结合来构建 URL，以下是一些关键的设计要点：

- **资源名使用名词且复数**：路径使用资源的名称（如 `users`、`products`），并使用复数形式。
- **使用 HTTP 方法来表示操作**：例如：
    - `GET /users`：获取用户列表
    - `POST /users`：创建用户
    - `PUT /users/{id}`：更新某个特定用户
    - `DELETE /users/{id}`：删除某个特定用户
- **路径层级关系应体现资源的从属关系**：
    - `GET /users/{id}/posts`：获取某个用户的所有文章
    - `GET /users/{id}/posts/{postId}`：获取某个用户的某篇文章

**示例**：

* GET /api/v 1/users         # 获取用户列表
* POST /api/v 1/users        # 创建新用户
* GET /api/v 1/users/{id}    # 根据用户 ID 获取用户信息
* PUT /api/v 1/users/{id}    # 更新用户信息
* DELETE /api/v 1/users/{id} # 删除用户

### 2.1. RESTful 路径设计的常见规则：

- **使用小写字母**：所有路径应采用小写字母，单词之间用 `-`（中划线）隔开。
- **版本控制**：通常在路径中加入版本号（如 `/api/v1`）来保证接口的兼容性。