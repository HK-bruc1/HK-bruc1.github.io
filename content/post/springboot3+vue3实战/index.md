---
title: Springboot3+vue3实战
date: 2024-04-10T17:35:23+08:00
lastmod: 2024-04-16
draft: true
image: cover.jpg
description: 接springboot
keywords: Springboot3+vue3实战
tags:
  - java
  - springboot
categories:
  - 工作
slug: 403f8e4d
---
## 项目架构
### 后台
- validation
- mybatis
- redis
- junit
- 项目部署
### 前端
- vite
- router
- pina
- element-plus
### 开发模式
- 前后端分离，都根据接口文档开发
## 环境搭建
- 准备数据库表
- 创建spring boot工程引入对应的依赖（web,mybatis,mysql）
- 配置文件application.yml中引入mybatis配置信息
- 创建包结构并准备实体类
## 创建springboot工程
- 手动创建spring boot工程（用idea模板）
- 在application中配置数据库信息
- 导入三个实体类（分别对应数据库三张表，封装从数据库拿到的信息）
## 设计用户功能模块
- 登录
- 注册
- 获取用户详细信息
- 更新用户基本信息
- 更新用户头像
- 更新用户密码
lombok:在编译阶段可以为实体类自动生成set和get方法以及tostring等。需要在pom文件中引入依赖。直接在实体类上使用注释@Data
### 注册
- 开发接口流程：
	1. 明确需求
	2. 阅读接口文档
	3. 思路分析
	4. 开发
	5. 测试
- 三层架构是一种常见的软件架构模式，通常包括以下三个层次：
	1. **表现层（Controller）**：
	    - 负责接收用户请求，并将请求转发给适当的处理器（Handler）进行处理。
	    - 解析用户请求中的参数和数据，并将其传递给服务层进行处理。
	    - 根据服务层处理的结果，选择合适的视图（View）进行展示，并将处理结果返回给用户。
	2. **业务逻辑层（Service）**：
	    - 包含应用程序的业务逻辑和核心功能。
	    - 负责处理业务逻辑，包括数据处理、业务规则的执行等。
	    - 通常调用持久化层（Mapper/DAO）来访问数据库或其他持久化存储。
	3. **持久化层（Mapper/DAO）**：
	    - **负责与数据存储进行交互**，通常是**数据库**。
	    - 提供对数据的持久化操作，如增删改查（CRUD）。
	    - 将业务逻辑层的请求转换成对数据库的操作，并将数据库的结果返回给业务逻辑层。
	在这种架构中，每一层都有明确定义的职责：
	- Controller 层**负责处理用户请求和响应**，**是与用户交互的入口**。
	- Service 层负责**业务逻辑的处理和控制**，是**核心的业务逻辑处理单元**。
	- Mapper/DAO 层负责**数据**持久化操作，包括**对数据库的访问和操作**。
	这种分层架构可以提高代码的可维护性和可扩展性，使得各个模块之间的耦合度降低，代码结构更清晰，易于理解和维护。
- 注解的说明：
	- **`@RestController`** 是 `@Controller` 和 `@ResponseBody` 注解的组合，表示该类是一个 RESTful 风格的控制器，并且所有的处理方法都会返回 JSON 或 XML 等数据格式，而不是视图。
		- 在 Spring MVC 中，`@RestController` 用于定义 RESTful API 的控制器类。它告诉 Spring 框架**这个类中的所有方法都会返回数据，而不是视图**。
		- 通常用于**构建 Web 服务或 RESTful API**，提供给客户端通过 HTTP 请求访问和操作数据的接口。
	- `@RequestMapping` 注解用于映射 HTTP 请求的 URL 和方法，表示该方法可以处理对 `/user` 路径的请求。
		- 在 Spring MVC 中，`@RequestMapping` 注解可以用于**类级别和方法级别**。当注解用于类级别时，表示该类中的所有方法都是以 `/user` 作为父路径的，而当用于方法级别时，表示该方法处理的请求路径为 `/user`。**可以通过参数来指定 HTTP 请求的方法、请求参数、请求头等条件**，来进一步精确地映射请求。
	- `@Autowired` 是 Spring 框架中最常用的**依赖注入**注解之一，它的作用是自动装配（注入）Bean。
		- **自动装配Bean**：Spring 在初始化时会自动扫描容器中的 Bean，并且**根据类型**（及其他条件）将匹配的 Bean 注入到被 `@Autowired` 注解标注的位置上。这样，在使用的时候就不需要手动创建和配置这些 Bean。
		- **简化依赖注入**：使用 `@Autowired` 注解可以避免手动注入 Bean 的繁琐过程，提高了代码的简洁性和可读性。
		- **使用 `@Autowired` 注解时，IoC 容器必须拥有相应类型的 Bean 对象，否则会导致自动装配失败，并抛出异常。**
	- `@Service` 注解除了表示一个类是服务类外，它也用于在 Spring IoC 容器中**声明 Bean 对象**。事实上，Spring 框架中有多个类似的注解，用于声明不同类型的 Bean 对象。
	- `@Mapper` 注解通常用于标识数据访问层（DAO 层）的接口，表示这个接口是一个 MyBatis 的映射器接口，用于**定义数据库操作的 SQL 语句和映射关系**
		- **声明 Mapper 接口**：通过 `@Mapper` 注解可以明确地将一个接口标识为 MyBatis 的映射器接口，以便在 MyBatis 框架中进行管理。
		- **自动扫描**：MyBatis 框架会扫描带有 `@Mapper` 注解的接口，并将其注册到 MyBatis 的映射器注册表中。在需要时，MyBatis 框架会自动创建这些接口的代理对象，并提供相应的数据库操作方法。
		- **代理实现**：`@Mapper` 注解会告诉 MyBatis 框架，需要为这个接口生成一个动态代理对象，在代理对象中实现数据库操作方法的具体逻辑。这样，我们就可以在接口中定义数据库操作方法，而无需编写具体的 SQL 语句和 JDBC 代码。
		- 在 MyBatis 的映射器接口中**只会包含抽象方法**，如**查询方法、插入方法、更新方法、删除方法**等，而不会包含方法的具体实现
		- 在 Spring Boot 中，通常情况下，如果 `@Mapper` 注解标注的 Mapper 接口所在的包路径在 Spring Boot 的默认扫描范围内（即主应用程序类所在的包及其子包），Spring Boot 会自动扫描这些包路径，发现带有 `@Mapper` 注解的接口，并将其注册为 Spring 容器中的 Bean 对象，从而可以被其他组件自动注入。**这样，在需要使用 Mapper 接口的地方，可以通过 `@Autowired` 注解来注入对应的 Mapper 实例。**
- **参数校验**（**spring提供了validation框架**）
	- 加判断语句很繁琐，参数多起来的话
	- 步骤：
		- 引入spring validation起步依赖
		- 在参数前面添加@pattern注解  （提供正则表达式）
		- 在controller类中添加@validated注解
	- 参数校验失败异常处理（参数校验失败返回的响应不合适）
		- **全局异常处理器**(创建一个类定义好异常响应形式)
```java
package com.itheima.excption;  
  
import com.itheima.pojo.Result;  
import org.springframework.util.StringUtils;  
import org.springframework.web.bind.annotation.ExceptionHandler;  
import org.springframework.web.bind.annotation.RestControllerAdvice;  
  
/**  
 * @author: Bruce  
 * @description: 全局异常处理  
 * @date: 2024/4/11 18:40  
 */
 @RestControllerAdvice  
public class GlobalExceptionHandler {  
    @ExceptionHandler(Exception.class)  
    public Result handleException(Exception e){  
        e.printStackTrace();  
        return Result.error(StringUtils.hasLength(e.getMessage())? e.getMessage() : "操作失败");  
    }  
}
```
- @RestControllerAdvice是一个用于全局异常处理的注解，它可以在整个应用程序中统一处理抛出的异常。通过使用该注解，可以在一个类中定义多个异常处理方法，并且这些方法可以针对不同的异常类型进行处理。
- @ExceptionHandler注解用于定义异常处理方法，它标识了一个方法用于处理特定类型的异常。在GlobalExceptionHandler类中，使用@ExceptionHandler(Exception.class)注解的handleException方法用于处理所有类型的异常。当抛出异常时，Spring会根据异常类型寻找匹配的异常处理方法，并将异常对象传递给该方法进行处理。
- 在handleException方法中，首先通过e.printStackTrace()方法将异常信息打印到控制台，以便进行调试。然后通过StringUtils.hasLength(e.getMessage())**判断异常对象是否包含消息内容**，如果包含则返回异常消息，否则返回默认的操作失败信息。最后，将异常信息封装成Result对象并返回给客户端。（你自定义了错误信息就按你的来，没有就默认显示操作失败）
- **先把整个功能的业务逻辑写好，在去写具体实现。这么写的好处就是可以利用idea自动生成方法的骨架。**
### 统一响应结果
- 为了规范符合请求响应的格式要求，设置一个统一的响应格式
```Java
package com.itheima.pojo;  

import lombok.AllArgsConstructor;  
import lombok.Data;  
import lombok.NoArgsConstructor;  
  
//统一响应结果  
@NoArgsConstructor  
@AllArgsConstructor //带参数和无参数构造方法  
@Data //为属性提供对外的访问方法  
public class Result<T> {  
    private Integer code;//业务状态码  0-成功  1-失败  
    private String message;//提示信息  
    private T data;//响应数据？？？往类中转入范型？  
  
    //快速返回操作成功响应结果(带响应数据)  
    public static <E> Result<E> success(E data) {  
        return new Result<>(0, "操作成功", data);  
    }  
  
    //快速返回操作成功响应结果  
    public static Result success() {  
        return new Result(0, "操作成功", null);  
    }  
  
    public static Result error(String message) {  
        return new Result(1, message, null);  
    }  
}
```
- `public static <E> Result<E> success(E data)`：
- `<E>`：这是一个泛型声明，表示这个方法是一个**泛型方法**，它有一个**类型参数 `E`**。这个类型参数用于表示**响应数据的类型**。
- `Result<E>`：这是方法的**返回类型**。它是一个**泛型类型**，表示返回的是一个 `Result` 对象，其中的 `data` 字段的类型是 `E`。
- `success(E data)`：这是方法的名称，表示成功操作的静态工厂方法。它接受一个类型为 `E` 的参数 `data`，表示成功操作的响应数据。
- 在这个方法中，使用了泛型 `<E>`，其中的 `E` 表示一个类型参数，它是一个占位符，表示可以是任意类型。在 `success` 方法中，你传入的 `data` 参数的类型就决定了 `E` 的具体类型。
**例如，如果你调用了 `success` 方法，并传入了一个 `String` 类型的数据，那么这个方法就会返回一个 `Result<String>` 类型的对象；如果传入的是一个 `Integer` 类型的数据，那么返回的就是一个 `Result<Integer>` 类型的对象。**
**这种泛型的设计使得 `Result` 类具有了更大的灵活性和通用性，可以适应各种不同类型的数据。**
### 登录
- 感觉写接口不用在意顺序，调用对应方向给出响应数据即可
- 如果不设置相关实体类，那么势必就要增加查询的代码，获取各种从数据库中取来的数据。有了实体类，直接用对外的set和get方法，方便很多。
- 登录逻辑中的jwt token令牌的作用是什么？
JWT（JSON Web Token）令牌是一种用于身份验证和授权的开放标准（RFC 7519），它可以在用户和服务之间安全地传输信息。在登录逻辑中，JWT 令牌的作用主要包括以下几点：
1. **身份验证：** JWT 令牌用于验证用户身份。当用户通过用户名和密码进行身份验证成功后，服务端会生成一个 JWT 令牌并返回给客户端。客户端在后续的请求中携带该令牌，**服务端可以通过验证 JWT 令牌的有效性来确认用户的身份。（一旦用户通过账号密码登录成功并获取了有效的 JWT 令牌，那么在该令牌有效期内，用户可以使用该令牌来访问受保护的资源，而无需再次提供账号密码。）**
2. **状态管理：** JWT 令牌可以包含用户的一些状态信息，如用户角色、权限等。服务端在生成 JWT 令牌时可以将这些信息加密在令牌中，**客户端在收到令牌后可以解析出这些信息，并在后续的请求中使用这些信息做出相应的处理。**
3. **无状态性：** JWT 令牌是无状态的，即服务端不需要在内存中保存任何关于用户会话的信息。每个 JWT 令牌都包含了足够的信息来验证用户的身份和权限，因此可以方便地在分布式系统中进行扩展和部署。
4. **跨域访问：** JWT 令牌可以跨域访问，即用户在**登录后可以通过携带 JWT 令牌访问不同域的服务**。这样可以简化跨域访问的处理流程，提高系统的灵活性和安全性。
- JWT（JSON Web Token）令牌由三部分组成，它们使用`.`进行分隔：
	- **Header（头部）**: 包含了令牌的元数据，通常包括两部分：令牌类型（typ）和使用的签名算法（alg）。
	- **Payload（载荷）**: 包含了一些声明（claims），它们是关于实体（例如用户）以及其他一些元数据的信息。声明分为三种类型：
		注册声明（Registered Claims）：预定义的一些声明，包括标准的声明和公开声明，比如`iss`（签发者）、`sub`（主题）、`exp`（过期时间）、`aud`（受众）等。
		私有声明（Private Claims）：由使用JWT的应用程序定义的声明，用于在JWT中传递非标准化的信息。
		公开声明（Public Claims）：用于在JWT中传递非敏感的标准化信息。
	- **Signature（签名）**: 使用头部中指定的算法对头部和载荷进行签名，以确保令牌的完整性和验证其来源。签名通常由使用的加密算法、密钥和消息的编码形成。
- 总的来说，JWT 令牌在登录逻辑中起到了身份验证、状态管理和安全传输信息的作用，它能够有效地帮助开发人员构建安全、可靠的身份验证和授权系统。(是一种规范，可以手写但不建议。)
```xml
<!-- jwt依赖-->  
<dependency>  
    <groupId>com.auth0</groupId>  
    <artifactId>java-jwt</artifactId>  
    <version>4.4.0</version>  
</dependency>
```
### 登录认证
- 在提供用户提起接口服务之前，应该先检查用户登录状态。
- @RequestMapping("/article")这个注解和@GetMapping("/list")的区别：
	`@RequestMapping("/article")`和`@GetMapping("/list")`是Spring MVC中的两种不同的映射方式。
	1. `@RequestMapping("/article")`是一个**通用的注解**，用于**将HTTP请求映射到控制器的处理方法上**。它可以用于映射各种类型的HTTP请求，包括**GET、POST、PUT、DELETE**等。在这个例子中，`@RequestMapping("/article")`表示将所有对"/article"路径的HTTP请求映射到对应的处理方法上。
	2. `@GetMapping("/list")`是`@RequestMapping`的特定用法之一，它表示将HTTP GET请求映射到控制器的处理方法上。与`@RequestMapping`相比，`@GetMapping`更加简洁，**专门用于处理GET请求**。
- **`@RequestMapping("/list")`注解表示当请求路径为`/list`时,映射的控制器处理方法会被执行**。
- 令牌就是一段字符串
	- 承载业务数据，减少后续请求查询数据库的次数
	- 防篡改，保证信息的合法性和有效性。（防伪功能）
	- jwt校验时使用的是签名密钥，必须和生成jwt令牌时使用的密钥是配套的
	- 如果jwt令牌解析校验时报错，则说明jwt令牌被篡改了或失效了，令牌非法。
```java
public Result<String> list(@RequestHeader(name = "Authorization") String token, HttpServletResponse response){  
    //验证登录状态token  
    try {  
        Map<String,Object> claims = JwtUtil.parseToken(token);  
        return Result.success("这是所有文章...");  
    } catch (Exception e) {  
        //响应状态码为401  
        response.setStatus(401);  
        return Result.error("未登录");  
    }  
}
```
- **第一部分：**
- - `@RequestHeader` 注解用于告诉 Spring MVC 框架，**该参数的值应该从请求头中获取。**
- `name = "Authorization"` 指定了请求头的名称，这里是 "Authorization"，它通常用于携带身份验证信息，比如 JWT（JSON Web Token）。
- `String token` 是方法的参数，它将接收到的 Authorization 头的值作为方法的输入。
- **第二部分：**
- 在 Spring MVC 中，`HttpServletResponse` 对象可以通过方法参数注入，就像 `@RequestHeader` 注解一样。当 Spring MVC 接收到请求并确定调用处理方法时，它会**自动将 `HttpServletResponse` 对象传递给方法。**
- 具体来说，Spring MVC 框架会自动检测方法参数类型，并尝试为其提供适当的实例。对于 `HttpServletResponse`，它会自动创建一个实例，并将当前的 HTTP 响应对象传递给方法。
- 在你的代码中，`HttpServletResponse response` **参数将自动获得当前请求的响应对象**。你可以使用该对象来设置响应的状态码或者进行其他与响应相关的操作。
- **第三部分：**
- 通常情况下，`JwtUtil.parseToken(token)` 方法在验证 JWT 令牌时如果遇到问题，比如令牌格式不正确、签名不匹配或者过期等，会抛出异常来表示验证失败。这是因为 JWT 的设计理念之一是将验证逻辑封装在库中，以提供简单的 API 接口来进行验证。
- 如果你直接抛出异常而没有捕获它，Spring MVC 框架可能会将其视为未处理的异常，并将其传递给全局异常处理器（如果有配置的话），或者返回一个默认的错误响应。这可能不是你想要的行为。
- 通过捕获异常并返回适当的错误响应，你可以更加精细地控制程序的行为，例如，你可以返回一个自定义的错误消息，设置特定的 HTTP 状态码，或者执行其他相关的操作。这种方式使得你能够更好地处理验证失败的情况，而不是简单地抛出异常。
- **疑问**
- 很多网站都有token令牌机制，那么本地存了很多网站的token，浏览器访问时怎么知道携带哪一个呢？
- 对于浏览器来说，它并不知道要携带哪个网站的令牌，而是由具体的网站通过发送的请求告知浏览器应该使用哪个令牌。具体来说，这涉及到以下几个方面：
	1. **请求的目标地址：** 当浏览器发送请求时，**请求中会包含目标地址**（URL）。根据请求的目标地址，浏览器知道是向哪个网站发送请求，从而可以确定应该使用该网站对应的令牌。
	2. **浏览器存储的令牌信息：** 浏览器通常会根据**用户登录时的操作将令牌信息存储在本地**，比如 Cookie、本地存储或者其他形式的存储介质中。当浏览器**发送请求时，它会检查本地存储的令牌信息，并将正确的令牌携带在请求中。**
	3. **网站的身份验证机制：** 网站通常会要求用户在登录时提供身份验证信息，并生成相应的令牌。**当用户访问需要身份验证的资源时，网站会要求用户提供相应的令牌。浏览器在发送请求时，会根据网站的要求将相应的令牌携带在请求中。**
- 浏览器在发送请求时会根据请求的目标地址和本地存储的令牌信息确定应该携带哪个令牌。**这些细节是由网站的前端和后端共同协调和处理的**，以确保请求能够正确地进行身份验证和授权。
### 拦截器
- 登录后，生成jwt token后，使用里面的每一个服务之前都要校验token，我以为是把校验程序封装起来调用，结果是使用拦截器。
- 使用拦截器进行 JWT token 的校验是一种常见的做法，它可以在**请求到达控制器之前（执行对应的处理方法之前或着说使用其他接口服务之前）对 JWT token 进行验证，确保请求的合法性。**这种做法有以下几个优点：
	1. **统一的验证逻辑：** 使用拦截器可以将 JWT token 的验证逻辑封装在一个地方，实现统一的验证逻辑。这样可以**避免在每个控制器中都编写相同的验证代码**，提高了代码的可维护性和可重用性。
	2. **解耦验证逻辑：** **将验证逻辑与控制器逻辑解耦**，使得**控制器专注于处理业务逻辑**而不用关心验证细节。这样可以提高代码的清晰度和可读性。
	3. **灵活性：** 通过拦截器可以灵活地控制验证逻辑的执行时机和范围，可以根据具体的需求对不同类型的请求进行不同的验证处理，从而满足不同场景下的需求。
	4. **全局配置：** 拦截器可以**通过配置实现全局生效，对所有的请求进行统一的验证处理**，从而确保整个应用的安全性。
- 总的来说，使用拦截器进行 JWT token 的校验是一种简洁、高效且易于管理的方式，可以有效地提高系统的安全性和可维护性。**封装验证逻辑并在每个控制器中调用并不是最佳实践，因为这样会导致代码冗余、可维护性差以及难以统一管理验证逻辑。相比之下，使用拦截器能够更好地实现统一的验证逻辑，并且提供了更灵活、清晰、可维护的解决方案。**
#### 定义一个拦截器对象
- 定义一个拦截器对象定义好拦截逻辑

```Java
package com.itheima.interceptors;  
  
import com.itheima.utils.JwtUtil;  
import jakarta.servlet.http.HttpServletRequest;  
import jakarta.servlet.http.HttpServletResponse;  
import org.springframework.stereotype.Component;  
import org.springframework.web.servlet.HandlerInterceptor;  
import java.util.Map;  
  
/**  
 * @author: Bruce  
 * @description: 登录状态拦截器  
 * @date: 2024/4/13 18:37  
 */
 @Component //bean对象注解声明  
public class LoginInterceptor implements HandlerInterceptor {  
    @Override  
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {  
        //验证令牌  
        //从请求中拿到token  
        String token = request.getHeader("Authorization");  
        //验证登录状态token  
        try {  
            Map<String,Object> claims = JwtUtil.parseToken(token);  
            //放行  
            return true;  
        } catch (Exception e) {  
            //响应状态码为401  
            response.setStatus(401);  
            //不放行  
            return false;  
        }  
    }  
}
```
- 将拦截器bean对象注入到IoC容器中，并声明在配置类中
```Java
package com.itheima.config;  
  
import com.itheima.interceptors.LoginInterceptor;  
import org.springframework.beans.factory.annotation.Autowired;  
import org.springframework.context.annotation.Configuration;  
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;  
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;  
  
/**  
 * @author: Bruce  
 * @description: 拦截器注册，放入IoC容器  
 * @date: 2024/4/13 20:16  
 */
 @Configuration  
public class WebConfig implements WebMvcConfigurer {  
    //自动装配一个bean对象到容器  
    @Autowired  
    private LoginInterceptor loginInterceptor;  
  
    //添加拦截器，直接添加对象即可  
    public void addInterceptors(InterceptorRegistry registry) {  
        registry.addInterceptor(loginInterceptor).excludePathPatterns("/user/login", "/user/register");  
    }  
}
```
### 获取用户的详细信息
- 登录成功后的主页有用户信息
- 个人中心也会有用户信息
- 直接用请求头中的token去解析拿到username（还有id,当时登录成功后发放令牌头部只携带了id和username）
- 根据username去查询用户的详细信息用user对象接受
- 在user类中的password上添加@JsonIgnore,让springmvc把数据转换为json格式时忽略password，为了安全。
- 表中的字段名是下划线组成的，但是类中的属性是驼峰式命名。那么那信息时系统不知赋值给谁，这时去要去配置文件中开启驼峰式与下划线的转换。
```yml
mybatis:  
  configuration:  
    map-underscore-to-camel-case: true
```
### threadLocal
- 我们在验证token时就解析过token了，那么可以复用吗？
	- userInfo和令牌验证时，虽然写法有一点区别，但是实现的功能是一样的即**从请求头中拿到token并解析**。
	- 场景：
		- 比如注册，用户通过浏览器访问路径后，处理方法一路从controller调到service再到mapper，假设三个层中都用到了每个参数，那么就要一直传参数这个操作。
		- 可以共享从拦截器中获取到的数据，复用到controller，service，mapper
	- 引入threadlocal（在拦截器解析完token后就可调用方法保存到threadLocal中，**实现线程内部共享**）
		- `ThreadLocal` 是 Java 中的一个特殊类，它提供了线程局部变量的功能。每个线程都有自己独立的 `ThreadLocal` 变量，线程之间互不影响。其作用主要有两点：
		- **线程隔离性**：每个线程都有自己独立的 `ThreadLocal` 实例，可以存储线程私有的数据，不同线程之间不会相互干扰。在多线程环境下，使用 `ThreadLocal` 可以避免线程安全问题。**(多个人访问数据互不干扰)**
		- **线程共享数据**：虽然 `ThreadLocal` 存储的数据是每个线程独享的，但是在同一个线程内部，可以通过 `ThreadLocal` 实例共享数据。这意味着，可以在一个线程内部的不同方法中共享数据，而**无需显式传递参数。**
	- 在你提到的场景中，可以使用 `ThreadLocal` 来存储从拦截器获取到的数据，然后在整个请求处理链中都能够访问这些数据，而无需在每个方法中显式传递。这样可以减少代码的冗余，提高代码的可读性和可维护性，同时降低了由于参数传递导致的错误发生的可能性。
- 定义一个类提供了对 `ThreadLocal` 的封装可以更方便地在应用程序中使用 `ThreadLocal`。
```Java
package com.itheima.utils;  
  
import java.util.HashMap;  
import java.util.Map;  
  
/**  
 * ThreadLocal 工具类  
 */  
@SuppressWarnings("all")  
public class ThreadLocalUtil {  
    //提供ThreadLocal对象,  
    private static final ThreadLocal THREAD_LOCAL = new ThreadLocal();  
  
    //根据键获取值  
    public static <T> T get(){  
        return (T) THREAD_LOCAL.get();  
    }  
      
    //存储键值对  
    public static void set(Object value){  
        THREAD_LOCAL.set(value);  
    }  
  
  
    //清除ThreadLocal 防止内存泄漏（当请求完毕的时候）  
    public static void remove(){  
        THREAD_LOCAL.remove();  
    }  
}
```
- 虽然 `ThreadLocal` 本身是一个线程局部变量，但是通过 `ThreadLocalUtil` 类的封装，可以更方便地操作 `ThreadLocal` 变量，而不需要直接操作 `ThreadLocal` 实例。这样可以提高代码的可读性和可维护性。
- **一个线程局部变量，但是在一个线程内部却相当于一个全局变量和单例模式的区别？**
	- 在一个线程内部使用 `ThreadLocal` 存储的数据确实在该线程内部表现为全局变量的特性，但不应将其与单例模式混淆。
	- 单例模式是一种设计模式，它确保一个类只有一个实例，并提供全局访问点。而 `ThreadLocal` 是 Java 中的一个类，它提供了线程局部变量的功能，即为每个线程都创建一个独立的变量副本，使得每个线程都可以独立地访问自己的变量副本，而不会与其他线程的变量副本产生冲突。
	- 虽然在单线程中，`ThreadLocal` 变量的行为类似于全局变量，但是它只在当前线程内部可见，不同线程之间的变量副本是相互独立的。因此，`ThreadLocal` 不能被称为单例，因为它并不是一个全局共享的单一实例，而是每个线程都有自己独立的副本。
- 单例模式使用场景：
	1. **日志记录器**：在应用程序中只有一个日志记录器实例可以确保所有的日志消息都被正确地记录，并且可以被全局访问。
	2. **数据库连接池**：在一个应用程序中，数据库连接池是一个重要的资源。通过使用单例模式可以确保只有一个数据库连接池实例，避免了资源浪费和性能问题。
	3. **配置信息**：在应用程序中，有时需要保存一些全局的配置信息，比如数据库连接信息、系统参数等。通过单例模式可以确保这些配置信息只被加载一次，并且可以被全局访问。
	4. **线程池**：在多线程应用程序中，线程池是一个常用的工具。通过使用单例模式可以确保只有一个线程池实例，避免了资源竞争和性能问题。
	5. **缓存管理器**：在应用程序中，缓存管理器可以用来缓存一些常用的数据，以提高系统的性能。通过使用单例模式可以确保只有一个缓存管理器实例，避免了数据不一致和性能问题。
#### 存数据在拦截器中我不奇怪，但是释放数据也在拦截器中，我不理解
- 在拦截器中释放数据的原因是为了确保线程局部变量（ThreadLocal）中存储的数据在请求处理完成后被正确清除，以避免内存泄漏或者数据污染的问题。
- 拦截器是在**请求被处理前和处理后执行的组件**，它可以用来**对请求进行预处理和后处理**。在预处理阶段（preHandle方法）中，我们可能会从请求中提取一些数据并存储到线程局部变量中，以便后续的处理方法可以使用这些数据。但是，在请求处理完成后，我们需要确保这些数据被正确清除，以免影响下一个请求的处理。
- 拦截器通过afterCompletion方法来知道请求处理已经完成。**这个方法在请求处理完成后被调用，不论请求处理是否成功或失败**。在该方法中，可以进行一些收尾工作，比如释放资源、清理线程局部变量等。
- 在Web应用中，请求处理完成通常意味着**请求已经被正确地处理，并且响应已经发送给了客户端**。但是，在这之后，客户端是否退出网址是由客户端自身的行为控制的，拦截器无法感知客户端的行为。拦截器只关心请求的处理过程，在请求被处理完成后，它会执行相应的后续操作。
### 更新用户基本信息
- 用户名和id不能修改
- `@PutMapping("/update")`：这是一个控制器方法的注解，表示该方法处理HTTP的PUT请求，并且映射到路径"/update"。PUT请求通常用于更新资源，这个方法似乎是用来更新用户基本信息的。
- `@RequestBody`：这个注解用于告诉Spring MVC将请求的HTTP主体（body）映射到方法的参数上。在这个方法中，它表示**将HTTP请求的主体（通常是JSON或XML格式）转换为User对象**，并将其作为参数传递给方法。这样，方法就可以获取到客户端发送的用户信息，并进行相应的处理。
- 使用这个服务必定是登录过的用户，而且用户信息都是从请求里面拿的，所以根据id来更新信息不会有错。但是我们使用postman时，请求中的user参数是自己定义的所以有一点bug：可以用别人用户id的token修改自己id的用户信息。
#### 优化(实体参数校验)
- 参数校验，还是用spring提供的validation框架（参数是一个实体对象，不是属性不能用@pattern注解，**直接去类中对应的属性上添加注解**）
- **在具体使用的地方写上@validated启用。要不然类的使用范围就大大缩短了。** （在下面有对应的解决方法）
- @NotNull   @Email   @NotEmpty,接口方法的实体参数上添加@validated启用
- **清楚注解的作用范围很重要**
```java
package com.itheima.pojo;  
  
import com.fasterxml.jackson.annotation.JsonIgnore;  
import jakarta.validation.constraints.Email;  
import jakarta.validation.constraints.NotEmpty;  
import jakarta.validation.constraints.NotNull;  
import jakarta.validation.constraints.Pattern;  
import lombok.Data;  
import lombok.NonNull;  
  
import java.time.LocalDateTime;  
@Data  
public class User {  
    @NotNull  
    private Integer id;//主键ID  
  
    private String username;//用户名  
  
    @JsonIgnore  
    private String password;//密码  
  
    @NotEmpty  
    @Pattern(regexp = "^\\s{1,10}$")  
    private String nickname;//昵称  
  
    @NotEmpty  
    @Email    private String email;//邮箱  
    private String userPic;//用户头像地址  
    private LocalDateTime createTime;//创建时间  
    private LocalDateTime updateTime;//更新时间  
}
```
### 更新头像
- 这段代码是一个 Spring MVC 控制器方法，用于处理 PATCH 请求，更新用户的头像。下面是对两个注解的解释以及路径变化的说明：
- `@PatchMapping("updateAvatar")`：`@PatchMapping` 是 Spring MVC 提供的注解之一，表示将该方法映射到处理 HTTP PATCH 请求的路由上。
- `("updateAvatar")` 指定了路由的路径为 "updateAvatar"。**由于没有以 `/` 开头，这个路径是相对路径，即相对于控制器的根路径。如果你的控制器的根路径是 `/user`，那么完整的路径将是 `/user/updateAvatar`。**
- `@RequestParam String avatarUrl`：`@RequestParam` 注解用于将 HTTP 请求中的参数映射到方法的参数上。在这个方法中，`avatarUrl` 参数表示从请求中获取名为 "avatarUrl" 的参数，并将其赋值给方法中的 `avatarUrl` 参数。
- 更新头像，根据拦截器中解析的id进行更新。
#### 两种获取系统时间的差别
- 这两种方法都可以用来获取更新时间，但是它们之间存在一些区别：
- 在 SQL 语句中使用 `update_time=now()`：这种方法是在执行 SQL 更新操作时，**在数据库层面直接设置更新时间**。这样做的好处是更新时间会准确地对应到数据库服务器的时间，无论是什么时候执行更新操作，都会使用数据库服务器的时间。**这种方法适用于需要确保更新时间的准确性，并且不需要在应用程序中对时间进行额外处理的情况。**
- 在应用程序中使用 `LocalDateTime.now()`：这种方法是在**应用程序的业务逻辑中获取当前时间**，并将其赋值给对象的更新时间属性。这样做的好处是可以**在应用程序中更灵活地控制时间的处理**，例如可以在**更新前对时间进行调整或者处理**。这种方法适**用于需要对时间进行额外处理或者定制化的情况，例如需要在更新前对时间进行一些逻辑判断或者处理。**
- 总的来说，如果只是**简单地记录更新时间**，并且不需要对时间进行额外处理，那么在 SQL 中直接设置更新时间会更方便和高效。如果**需要对时间进行额外处理或者定制化**，那么在应用程序中获取当前时间并进行处理会更适合。
区别：**获取到了用户信息赋值到了user对象以及没有信息只有id和图床连接只能用now()`
- 数据校验：`@URL` 是 Java Bean Validation（JSR 380）中的一个约束注解之一，它用于验证一个字符串是否符合 URL 的格式。具体来说，它会检查被注解的字段是否是一个有效的 URL。使用 `@URL` 注解时，被注解的字段必须是一个字符串类型（String），并且它会验证该字符串是否是一个有效的 URL。如果不是有效的 URL，则验证将失败，并且会触发相应的验证错误。
### 更新用户密码
- 接受请求中body中的参数，然后校验是否符合要求，最后写入数据库。
## 文章分类功能设计
### 新增文章分类
- 一样的实现逻辑，前端传来的数据和具体写入数据库的数据要区分（可能要补充属性再插入）
- 我的控制层代码如下：我的新增文章分类不设置具体的映射路径，但是加了注解，那么请求/category时，会映射到这个处理方法上吗？
```Java
@RestController 
@RequestMapping("/category") 
public class CategoryController { 
//调用service层的方法，要先注入一个bean对象（此前要声明一个bean对象） @Autowired private CategoryService categoryService; 
//新增文章分类 
@PostMapping 
public Result add(@RequestBody Category category){          categoryService.add(category); 
	return Result.success(); } }
```
- 在你提供的代码中，`CategoryController` 类上使用了 `@RequestMapping("/category")` 注解，而在 `add` 方法上只使用了 `@PostMapping` 注解，没有指定具体的路径。这意味着 `add` 方法会处理所有 `POST` 请求，且请求路径是相对于 `CategoryController` 类上的 `/category` 路径的。因此，**当你发送一个 `POST` 请求到 `/category` 路径时，会映射到 `add` 方法上进行处理。**
- 如果你想要限定 `add` 方法只处理 `/category` 路径的 `POST` 请求，可以在 `@PostMapping` 注解中指定具体的路径，例如：
```Java
@PostMapping("/add")
public Result add(@RequestBody Category category){
    categoryService.add(category);
    return Result.success();
}
```
**这样，`add` 方法只会处理 `/category/add` 路径的 `POST` 请求。**
- 参数校验：**实体类参数去类中添加注解并在方法处开启**
### 文章分类列表
- 请求路径是跟新增文章分类一样的“/category”
- 他们的区分方式就是各自的请求方式不一样，一个为post一个为get。
- 通过各自的不同请求方式来映射不同的控制层处理方法
- 返回的时间格式不符合要求
	- 因为返回结果是要把数据转换为Category实例对象的json格式的。
	- 要想对属性限制只好去类中约束
### 获取文章分类详情
- 用户点击分类中的编辑按钮时，会弹出弹窗，显示当前分类的名称和别名。
- 通过前端传过来的分类id查看
- 假设请求方式是get，localhost:8080/category/detail?id=1
- 那么映射到的处理方法应该是这样的：
```Java
//查看分类详情（通过分类id）  
@GetMapping("/detail")  
public Result<Category> detail(Integer id){  
   Category c =  categoryService.findById(id);  
   return Result.success(c);  
}
```
- **处理方法的形参名字不能乱改，和前端传入的参数名一致，不然处理方法找不到参数传入**
### 更改文章分类
- 点击文章分类编辑按钮后弹窗弹出当前分类的分类详情后，可以修改再提交以达到更改文章分类的目的。
- @NotNull和@NotEmpty的区别：
 1. `@NotNull`：
    - `@NotNull` 注解用于验证一个对象属性的值是否为 null。
    - 当你在一个字段上添加了 `@NotNull` 注解时，它表示该字段的值**不能为空，不能为 null。**
    - 通常用于验证引用类型的属性，例如对象、集合等。
2. `@NotEmpty`：
    - `@NotEmpty` 注解用于验证一个对象属性的值是否为空。
    - 当你在一个字段上添加了 `@NotEmpty` 注解时，它表示该**字段的值不能为空，并且不能为空字符串、空集合或者空数组。**
    - 通常用于验证字符串、集合或者数组类型的属性。
- 这是mapper层的代码，我很好奇方法传入一个实例对象，使用sql时可以直接访问对象中的属性？
```Java
//更改文章分类  
@Update("update category set category_name=#{categoryName},category_alias=#{categoryAlias},update_time=#{updateTime} where id=#{id}")  
void update(Category category);
```
- 在 MyBatis 中，确实可以直接访问对象中的属性。MyBatis 在处理参数对象时，会根据对象的属性名自动映射到 SQL 语句中的参数。这种方式称为**基于对象的参数映射。**
- `update` 方法接受一个 `Category` 对象作为参数，然后在 SQL 语句中使用 `#{}` 占位符来引用对象的属性。这样，在执行 SQL 语句时，**MyBatis 会自动将 `Category` 对象中对应的属性值填充到 SQL 语句中的相应位置**，从而完成参数的绑定和执行。
- **想要使用类名来调用属性呢？** （假设参数来自不同对象）
- 在 MyBatis 中，可以**使用类名来调用属性**，但是需要结合 MyBatis 的 `@Param` 注解。通常情况下，MyBatis 会将参数对象的属性映射到 SQL 中，**但是如果参数对象是一个复杂类型（例如包含多个属性的类），或者你希望在 SQL 中使用不同于参数对象的属性名**，那么就需要使用 `@Param` 注解来**显式地指定参数**。
```Java
void update(@Param("category") Category category);
```
- 然后在 SQL 中使用 `#{category.categoryName}`、`#{category.updateTime}` 等来引用类 `Category` 中的属性。
- 需要注意的是，`@Param` 注解中的参数名（例如上面的 "category"）需要和 SQL 中的参数名保持一致。
#### 分组校验
- **实体对象参数校验时，都是在类中添加注解的方式。问题是当有两个处理方法都用到了实体参数校验但是各自的校验内容不一样。而都是用@validated启动的，就会导致校验冲突。**
- 比如说新增文章分类是不需要传入分类id的，因为会自动增加。
- 但是更新文章分类确实需要传入分类id的，不进行分组校验坑定会有冲突。
- **解决方法：**
- 把校验项进行归类分组，在完成不同功能时，校验指定组中的校验项。
	- 定义分组
	- 在属性的校验上归属分组
```java
package com.itheima.pojo;  
  
import com.fasterxml.jackson.annotation.JsonFormat;  
import jakarta.validation.constraints.NotEmpty;  
import jakarta.validation.constraints.NotNull;  
import lombok.Data;  
import java.time.LocalDateTime;  
  
@Data  
public class Category {  
    @NotNull(groups = Update.class)  
    private Integer id;//主键ID  
    @NotEmpty(groups = {Update.class, Add.class})  
    private String categoryName;//分类名称  
    @NotEmpty(groups = {Update.class, Add.class})  
    private String categoryAlias;//分类别名  
    private Integer createUser;//创建人ID  
    @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss", timezone = "GMT+8")  
    private LocalDateTime createTime;//创建时间  
    @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss", timezone = "GMT+8")  
    private LocalDateTime updateTime;//更新时间  
  
    //定义分组（接口名怎么开头是大写？）  
    public interface Add{  
  
    }  
    public interface Update{  
  
    }  
}
```

- 校验时启用对应分组即可
```java
//更改文章分类（从前端请求中获取参数，只有id，分类名，别名。创建时间和更新时间没有，需要补充）  
@PutMapping  
public Result update(@RequestBody @Validated(Category.Update.class) Category category){  
    categoryService.update(category);  
    return Result.success();  
}

//新增文章分类  
@PostMapping  
public Result add(@RequestBody @Validated(Category.Add.class) Category category){  
    //参数校验  
    categoryService.add(category);  
    return Result.success();  
}
```
- **改进方案**：
- **指定校验项归属分组时，只指定不同的，相同就不指定让他归属默认分组，然后定义分组时继承默认分组即可（继承默认组中所有的校验项）。**
### 删除文章分类（独立完成）
- 写controller层的方法，参数校验
- **知道校验为什么没有生效吗？？？**
- @Validated(Category.DeleteCategory.class)**给实体类参数用的**，**实体类对象参数校验通常是在实体类上使用注解才会生效。对于基本数据类型（如 `Integer`、`Long` 等）作为方法参数的情况，Spring MVC 不会执行参数对象的校验。**
- 因此，对于**基本数据类型的方法参数，你需要使用 `@NotNull`、`@Min`、`@Max` 等注解来直接对其进行校验**，而不是使用实体类对象的校验注解。
- **`@Pattern` 注解通常用于对字符串类型的属性进行格式校验，例如验证邮箱、电话号码等。对于整数类型的属性，通常使用 `@Min`、`@Max` 等注解进行范围校验。**
- 如果你希望对整数类型的属性进行格式校验，例如要求其必须是某种特定格式的数字字符串，你也可以使用 `@Pattern` 注解，但是需要注意一些细节。因为 `@Pattern` 注解的 `regexp` 属性是一个正则表达式，所以你需要编写一个匹配整数的正则表达式，并将其作为参数传入。
- 例如，如果你想要验证 `id` 必须是 1 到 999 之间的数字。
- 改进：
```Java
//删除文章分类（直接从请求参数中拿）  
@DeleteMapping  
public Result deleteCategory(@NotNull(message = "id不能为空！") Integer id){  
    categoryService.deleteCategory(id);  
    return Result.success();  
}
```