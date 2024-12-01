---
date: '2024-11-30T12:46:50+08:00'
title: 'Spring中Validation注解使用'
draft: false

tags: ["spring"]
categories: ["spring"]
---


在日常开发中，参数校验是一个常见需求，而 Java 的 **Bean Validation** 提供了一种优雅的方式，通过注解对对象的字段进行校验。Spring 对此功能进行了深度整合，使得在 Controller、Service 等层面实现校验变得非常简单。

本文将从以下几个方面介绍如何在 Spring 中使用 Validation 注解：

1. 引入依赖  
2. 简单示例  
3. 常见校验注解分类与说明  
4. 分组校验  
5. 自定义校验  

---

## 1. 引入依赖

在使用 Spring 校验功能之前，需要引入相关依赖。  
通常使用 Hibernate Validator 作为 JSR 380 的实现。

### Maven

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

### Gradle

```groovy
implementation 'org.springframework.boot:spring-boot-starter-validation'
```

---

## 2. 简单示例

以下是一个基本的参数校验示例。我们通过 `@NotNull`, `@Size` 等注解对参数进行校验，并在校验失败时返回错误信息。

### 数据模型

```java
import javax.validation.constraints.NotNull;
import javax.validation.constraints.Size;

public class User {
    @NotNull(message = "用户名不能为空")
    @Size(min = 3, max = 15, message = "用户名长度必须在3到15个字符之间")
    private String username;

    @NotNull(message = "密码不能为空")
    @Size(min = 6, message = "密码长度至少为6个字符")
    private String password;

    // Getter & Setter
    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}
```

### Controller

```java
import org.springframework.validation.annotation.Validated;
import org.springframework.web.bind.annotation.*;

import javax.validation.Valid;

@RestController
@RequestMapping("/users")
@Validated
public class UserController {

    @PostMapping("/register")
    public String register(@RequestBody @Valid User user) {
        return "用户注册成功：" + user.getUsername();
    }
}
```

### 测试

请求示例：

#### 请求 Body
```json
{
    "username": "john",
    "password": "123456"
}
```

#### 响应成功
```
用户注册成功：john
```

#### 错误请求 Body
```json
{
    "username": "jo",
    "password": ""
}
```

#### 响应失败
```json
{
    "timestamp": "2024-11-18T12:34:56.789",
    "status": 400,
    "error": "Bad Request",
    "message": "用户名长度必须在3到15个字符之间; 密码不能为空"
}
```

---

## 3. 常见校验注解分类与说明

### 通用校验

| 注解        | 功能说明             | 示例                        |
| ----------- | -------------------- | --------------------------- |
| `@NotNull`  | 字段不能为空         | `@NotNull(message="必填")`  |
| `@NotBlank` | 字符串非空且非空白   | `@NotBlank(message="必填")` |
| `@NotEmpty` | 集合或数组不能为空   | `@NotEmpty`                 |
| `@Size`     | 字符串、集合长度校验 | `@Size(min=1, max=10)`      |

### 数值校验

| 注解              | 功能说明             | 示例              |
| ----------------- | -------------------- | ----------------- |
| `@Min`            | 值必须大于等于指定值 | `@Min(18)`        |
| `@Max`            | 值必须小于等于指定值 | `@Max(100)`       |
| `@Positive`       | 值必须为正数         | `@Positive`       |
| `@PositiveOrZero` | 值必须为正数或零     | `@PositiveOrZero` |
| `@Negative`       | 值必须为负数         | `@Negative`       |

### 字符串校验

| 注解       | 功能说明           | 示例                               |
| ---------- | ------------------ | ---------------------------------- |
| `@Email`   | 必须是合法邮箱地址 | `@Email(message="邮箱格式错误")`   |
| `@Pattern` | 必须匹配正则表达式 | `@Pattern(regexp="\\d{3}-\\d{3}")` |

### 日期校验

| 注解               | 功能说明             | 示例               |
| ------------------ | -------------------- | ------------------ |
| `@Past`            | 必须是过去的日期     | `@Past`            |
| `@Future`          | 必须是将来的日期     | `@Future`          |
| `@PastOrPresent`   | 必须是过去或当前日期 | `@PastOrPresent`   |
| `@FutureOrPresent` | 必须是将来或当前日期 | `@FutureOrPresent` |

>Validation关于直接对JSON的日期格式进行校验，需要使用正则表达式 @Pattern(regexp = "")或者自定义注解，建议直接使用Jackson的@JsonFormat。

---



## 4. 分组校验

在实际项目中，不同场景可能需要不同的校验规则，例如新增和更新时字段要求可能不同。可以通过 **分组校验** 实现。

### 分组接口

```java
public class Group{
public interface CreateGroup {}
public interface UpdateGroup {}
}
```



### 数据模型

```java
import javax.validation.constraints.*;

public class User {
    @NotNull(message = "用户ID不能为空", groups = Group.UpdateGroup.class)
    private Long id;

    @NotBlank(message = "用户名不能为空", groups = Group.CreateGroup.class)
    private String username;

    @NotBlank(message = "密码不能为空", groups = GroupCreateGroup.class)
    private String password;

    // Getter & Setter
}
```

### Controller

```java
import org.springframework.validation.annotation.Validated;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
@Validated
public class UserController {

    @PostMapping("/create")
    public String create(@RequestBody @Validated(CreateGroup.class) User user) {
        return "创建成功：" + user.getUsername();
    }

    @PostMapping("/update")
    public String update(@RequestBody @Validated(UpdateGroup.class) User user) {
        return "更新成功：" + user.getId();
    }
}
```

---

## 5. 自定义校验

当现有的注解无法满足需求时，可以自定义校验注解。

### 自定义注解

```java
import javax.validation.Constraint;
import javax.validation.Payload;
import java.lang.annotation.*;

@Documented
@Constraint(validatedBy = UsernameValidator.class) // 关联校验器
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
public @interface ValidUsername {
    String message() default "用户名非法";

    Class<?>[] groups() default {};

    Class<? extends Payload>[] payload() default {};
}
```

### 自定义校验器

```java
import javax.validation.ConstraintValidator;
import javax.validation.ConstraintValidatorContext;

public class UsernameValidator implements ConstraintValidator<ValidUsername, String> {
    @Override
    public boolean isValid(String value, ConstraintValidatorContext context) {
        return value != null && value.matches("^[a-zA-Z0-9]+$");
    }
}
```

### 使用自定义注解

```java
public class User {
    @ValidUsername
    private String username;

    // Getter & Setter
}
```

