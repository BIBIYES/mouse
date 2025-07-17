## 1. 什么是 `mybatis-plus`
`mybatis-plus` 是一个数据库持久层框架
为我们提供了便捷的数据库操作方法，可以直接继承框架写好的方法，直接操作数据库
简化了 `jdbc` 繁琐的数据库操作
## 2. 引入坐标 (依赖)
要正确使用 `mybatis-plus`
在 `pom.xml` 中引入它的的坐标
```xml
<!-- https://mvnrepository.com/artifact/com.baomidou/mybatis-plus-boot-starter -->
<dependency>  
    <groupId>com.baomidou</groupId>  
    <artifactId>mybatis-plus-boot-starter</artifactId>  
    <version>3.5.3.1</version>  
</dependency>  
<!-- https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->  
<dependency>  
    <groupId>com.mysql</groupId>  
    <artifactId>mysql-connector-j</artifactId>  
    <version>8.3.0</version>  
</dependency>  
<!-- https://mvnrepository.com/artifact/com.alibaba/druid-spring-boot-starter -->  
<dependency>  
    <groupId>com.alibaba</groupId>  
    <artifactId>druid-spring-boot-starter</artifactId>  
    <version>1.2.19</version>  
</dependency>
```

> [!tips] 提示
> 如果你引入了 `Mybatis-Plus` 你可以直接使用 `Mybatis` 因为他继承了
> 请一定要注意版本信息，这可能会导致报错，建议使用 springboot 版本 `2x`
> 当前工程目录创建的版本是 `jdk8` `Spingboot2.7.6版本`

## 3. Mybatis-Plus 配置
我们需要在 `application.yaml` 中配置
```yaml
spring:  
  datasource:  
	// 数据源类型
    type: com.alibaba.druid.pool.DruidDataSource  
	// 数据库驱动
    driver-class-name: com.mysql.cj.jdbc.Driver  
    // 数据库连接地址
    url: jdbc:mysql://localhost:3306/good_learn_ai?useSSL=false  
    // 数据库用户名
    username: root
    // 数据库密码  
    password:  
mybatis-plus:  
  configuration:
    // 日志输出类型
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
```

## 4. 使用 `mybatis-plus` 注解的方式去操作数据库
1. 通过表中**指定的字段**来查找数据
比如说我们要通过表中的 `student_id` 来查询数据
```java
@Select("select * from student_exam_paper where student_id = #{studentId}")  
List<StudentExamPaper> getExamPapersByStudentId(Long studentId);
```
2. 通过表中的**模糊查询**来查找数据
比如说我们要通过 `exam_paper_name` 进行模糊查询，查找试卷名包含某个关键词的数据
```java
@Select("select * from exam_paper where exam_paper_name like CONCAT('%', #{keyword}, '%')") List<ExamPaper> getExamPapersByNameKeyword(@Param("keyword") String keyword);
```
3. 通过表中**多个字段**来查找数据
比如说我们要通过 `student_id` 和 `exam_paper_id` 同时查询数据
```java
@Select("select * from student_exam_paper where student_id = #{studentId} and exam_paper_id = #{examPaperId}")
List<StudentExamPaper> getStudentExamPaperByStudentIdAndExamPaperId(@Param("studentId") Long studentId, @Param("examPaperId") Long examPaperId);

```

### 4.1. 联表查询
**联表查询**
*同时查询多个表里的数据*
假设我们有两个表：

- `student_exam_paper`：记录学生加入的试卷。
- `exam_paper`：记录试卷的详细信息。

我们想要查询某个学生加入的试卷及其详细信息（试卷名称、创建时间等）。
**使用普通的查询会非常浪费时间**
1. 普通的查询先要**获取自己加入的所有试卷**拿到所有自己加入的**试卷 `id`**
2. 在通过**试卷id**来查询所有试卷的详情信息
这样会非常浪费时间

### 4.2. 多表查询 `sql` 示例
```sql
SELECT student_exam_paper.*, exam_paper.exam_paper_name, exam_paper.creation_date
FROM student_exam_paper
JOIN exam_paper ON student_exam_paper.exam_paper_id = exam_paper.exam_paper_id
WHERE student_exam_paper.student_id = 1;

```
#### 4.2.1. `SELECT student_exam_paper.*, exam_paper.exam_paper_name, exam_paper.creation_date`

- **`SELECT`**：表示你想要从数据库中获取哪些列。
- **`student_exam_paper.*`**：使用 `*` 表示你想要选择 `student_exam_paper` 表中的所有列。比如，`student_exam_paper` 表可能包含的列有 `student_id`、`exam_paper_id`、`joined_date` 等。这里的 `student_exam_paper.*` 就会返回所有这些列。
- **`exam_paper.exam_paper_name`**：你想从 `exam_paper` 表中获取 `exam_paper_name` 这列。也就是试卷的名称。
- **`exam_paper.creation_date`**：你想从 `exam_paper` 表中获取 `creation_date` 这列。也就是试卷的创建日期。

#### 4.2.2. `FROM student_exam_paper`

- **`FROM`**：表示你要从哪个表中进行查询。这一行表示从 `student_exam_paper` 表中开始查询数据。

#### 4.2.3. `JOIN exam_paper ON student_exam_paper.exam_paper_id = exam_paper.exam_paper_id`

- **`JOIN`**：这表示你想将另一个表 (`exam_paper`) 与 `student_exam_paper` 进行连接查询。
- **`ON student_exam_paper.exam_paper_id = exam_paper.exam_paper_id`**：这是 `JOIN` 的条件。也就是说，你要将 `student_exam_paper` 表中的 `exam_paper_id` 和 `exam_paper` 表中的 `exam_paper_id` 进行匹配，只有匹配的行会被连接起来返回结果。这个 `exam_paper_id` 字段是 `student_exam_paper` 表和 `exam_paper` 表之间的**外键**，用于表示学生参加的是哪张试卷。

#### 4.2.4. `WHERE student_exam_paper.student_id = 1`

- **`WHERE`**：用来指定查询的条件。只有满足条件的行才会被返回。
- **`student_exam_paper.student_id = 1`**：这意味着你只想要 `student_exam_paper` 表中 `student_id` 为 `1` 的行，也就是说，查询出**学生 ID 为 1** 的学生所加入的试卷信息。



### 4.3. 多表查询
多表关联查询，在我们的关系型数据库中，[[#ORM]] 类的设计**会有一些差异**
为了实现复杂的关系型映射 `mybatis` 提供了
* `@Results`
	* 代替 `<resultMap>` 标签，该注解中可以加入单个或多个 `Results` 注解
* `@Result`
	* `column`
		* 数据表中的字段名
	* `property`
		* 类中对应的属性名
* `@One`
	* 代替 `<assocations>` 标签，用于指定查询中返回的单一对象，通过 `select` 属性指定英语多表查询的方法 [[#`@One` 使用方法 | 使用方法]]
* `@Many`
	* 代替 `<collection>`标签，用于指定查询中返回的集合对象 [[#`@Many`| 使用方法]]
### 4.4. `@One` 使用方法
```java
@Result(column="",property="",one=@One(select=""))
```
### 4.5. `@Many` 使用方法
```java
@Result(column="",.property="",many=@many(select=""))
```
### 4.6. 多表查询快速上手
**用户查询订单**
1. 我们需要在 [[#ORM]] 创建一个 `user` 实体类并且预留一个 `OrderList` 商品列表变量
```java
@TableField(exist = false)  
private List<Orderinfo> orderinfoList;
```
> 你可以使用 `@TableField(exist = false)` 是这个变量隐藏，可以防止调用 mybatis-plus 中的快速**增删改查**接口失效

2. 我们需要在 `OrderMapper` 提供一个通过 `id` 查询商品订单列表的接口
```java
public interface OrderInfoMapper extends BaseMapper<Orderinfo> {  
    // 通过用户id来查询订单  
    @Select("SELECT * FROM orderinfo where uid =#{uid}")  
    List<Orderinfo> getUserOrderInfo(int uid);
```
3. 其原理就是我们在获取用户信息的时候**一起调用了**获取商品列表的**方法**
![[Pasted image 20240330161331.png]]
### 4.7. 条件查询
`mybatis` 提供了一些条件的方法，可以免除书写 `sql` 快速的根据**条件去查询信息**
[[https://baomidou.com/pages/10c804/#abstractwrapper|前往官方文档]]
```java
@GetMapping("/getUserByName")  
public List<User> getUserByName(String uname){  
    QueryWrapper<User> queryWrapper = new QueryWrapper<>();  
    queryWrapper.eq("uname",uname);  
    return  userMapper.selectList(queryWrapper);  
    // 通过用户名来查询用户信息
}
```
### 4.8. 分页显示
如果你要使用分页显示
**你需要引入这个包**
```xml
<!-- https://mvnrepository.com/artifact/com.github.pagehelper/pagehelper-spring-boot-starter -->
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.3.0</version>
</dependency>
```
然后你需要配置这个包的配置文件
```java
# 分页查询配置  
pagehelper.helper-dialect=mysql  
pagehelper.reasonable=true  
pagehelper.support-methods-arguments=true  
pagehelper.params=count=countSql
```
**分页显示**对*请求*的参数会有要求
> 分页显示需要传递两个参数
> `pageSize` 和 `pageNum`
> 分别对应 **一页显示多少**，**当前处于多少页**

```js
{
        name: '',
        phone: '',
        pageNum: 1,
        pageSize: 20,
}
// 这个请求参数携带了`name` 和 `phone` 还有 当前页数 和 要求一页给出来多少数据的数量

```
**分页显示**对*响应*参数会有要求
>你需要对分页显示响应的数据用 `PageInfo` 来封装一个带有页面数据的 `List`
```java
public PageInfo<Admin> getUser(AdminParams adminParams) {  
//      System.out.println(params);  
        Integer pageNum = adminParams.getPageNum();  
        Integer pageSize = adminParams.getPageSize();  
        System.out.println(pageNum + " " + pageSize);  
        PageHelper.startPage(pageNum, pageSize);  
        List<Admin> list = adminMapper.selectList(null);  
        return PageInfo.of(list);  
    }
```
> 返回给前端的数据可以用来绑定