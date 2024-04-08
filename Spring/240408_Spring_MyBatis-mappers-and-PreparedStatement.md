## MyBatis mappers and PreparedStatment

### Source Code

- Before Resolution
```java
<select id="exampleId" resultMap="exampleMap" parameterType="String">
    SELECT * 
    FROM example_table
    WHERE attribute 
        LIKE CONCAT("%#{attribute}%");
</select>

```

- After Resolution
```java
<select id="exampleId" resultMap="exampleMap" parameterType="String">
    SELECT * 
    FROM example_table
    WHERE attribute 
        LIKE CONCAT("%", #{attribute}, "%");
</select>
```

### Explanation

**Start Point**

In using `MyBatis` with `Spring Framework`, I wrote `.xml` files for mapping. The elements written in the file include a SQL query in itself. I've met a problematic situation while executing a query with a `WHILE ... LIKE ...` clause. The point is that `#{attribute}` was not applied to the expression following the `LIKE` operator. The source code above exemplifies my problematic code and the resolution.

Before resolving the problem, the statment printed by `jdbc.BaseJdbcLogger` looked like `... LIKE "%?%"`. In a while, I did not found what was wrong in my statment. Then, I found out i was using `#{}` in the quoted expression. I tried concatenating the `#{}` with `%` wild cards. It worked and printed a valid result.

What I wondered was how `PreparedStatement` works, as I've studied that `MyBatis` mapper elements are transformed to `PreParedStatement` Object. It's time to analyze the code.

**Tackling Curiosity**

1. `#{ }` parameter explained

Parameters expressed with `#{ }` are passed into the `PreparedStatement` instance in an order. The `MyBatis` offical document illustrates this process with an example code. Let's start with a `select` mapper element.

```xml
<!-- the codes below are fetched from the mybatis official guide -->
<!-- https://mybatis.org/mybatis-3/sqlmap-xml.html --> 
<select id="selectPerson" parameterType="int" resultType="hashmap">
  SELECT * FROM PERSON WHERE ID = #{id}
</select>
```

Here, the paramter required in `selectPerson` statement is wrapped in `#{ }` notation. The statement above would be written in `JDBC` as following.

```java
// Similar JDBC code, NOT MyBatis…
String selectPerson = "SELECT * FROM PERSON WHERE ID=?";
PreparedStatement ps = conn.prepareStatement(selectPerson);
ps.setInt(1,id);
```

A notable part is that the position of the parameter is identified as `?`. Also, the argument `id` is passed to the `ps` after the initialization. However, would this be a exact transformation process? Remember that the comment in the code above points that it's just a similar code.

2. How `MyBatis` parse the `#{}` notation

In-process.

### References 

https://mybatis.org/mybatis-3/sqlmap-xml.html

https://github.com/mybatis/mybatis-3/blob/5a53aa48c696518526d7c9a0548e2ebdc8452d4a/src/main/java/org/apache/ibatis/builder/SqlSourceBuilder.java#L46