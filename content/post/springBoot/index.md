---
title: SpringBoot
date: 2024-04-09T12:24:44+08:00
lastmod: 2024-04-10
draft: false
image: cover.jpg
description: 记录springBoot的学习疑惑
keywords: springBoot
tags:
  - java
  - springboot
categories:
  - 工作
slug: 8c6001d1
---
## springBoot的作用（chatgpt）
- Spring Boot可以让Spring、Spring MVC、MyBatis等框架的使用更加方便。通过Spring Boot，开发者可以快速搭建项目，并且无需过多地关注繁琐的配置细节。Spring Boot通过自动配置、内嵌容器、简化的依赖管理等功能，简化了开发流程，提高了开发效率。因此，很多开发者选择使用Spring Boot来构建项目，以便更加专注于业务逻辑的实现，而不必花费太多精力在配置上。
- 学习Spring Boot之前并不需要先学习SSM框架，因为Spring Boot本身并不是一种新的框架，而是对Spring、Spring MVC、MyBatis等框架的简化和增强。如果你已经对Java编程有一定的了解，那么直接学习Spring Boot也是完全可行的。
- 如果你想快速入门并且更关注现代化的开发方式，那么直接学习Spring Boot可能更合适；如果你想全面了解Java企业级开发的主流技术栈，那么学习SSM框架也是有意义的。
- 找工作需要，先学。
### 目标
1. spring boot3
2. vue3
3. 单体应用中前后端常用的技术
4. 独立完成管理系统的接口开发和页面开发
5. web开发常见的解决方案
### 传统方式构建Spring应用程序和使用Spring Boot构建Spring应用程序
- **区别如下**：
1. **配置方式：**
    - 传统方式：传统Spring应用程序需要**手动配置各种组件**，如数据源、事务管理器、MVC配置等，通常使用**XML配置文件**（如配置bean）或Java配置类进行配置。
    - Spring Boot：Spring Boot采用约定大于配置的原则，通过自动配置功能，大大简化了配置过程。开发者只需提供少量的配置，Spring Boot就能根据约定自动配置所需的组件，**无需手动配置大量的XML文件**或Java类。
2. **依赖管理：**
    - 传统方式：传统Spring应用程序需要**开发者手动管理依赖的版本和配置（确实需要引入对应版本）**，通常使用**Maven**或Gradle等构建工具来管理依赖。
    - Spring Boot：Spring Boot引入了Starter依赖的概念，简化了依赖管理的过程。开发者**只需引入相应的Starter依赖**，Spring Boot会自动管理所需的依赖版本和配置。
3. **内嵌容器：**
    - 传统方式：传统Spring应用程序需要**手动部署到外部的Servlet容器**（如**Tomcat**、Jetty等）中运行。
    - Spring Boot：Spring Boot集成了多种内嵌的Servlet容器（如Tomcat、Jetty、Undertow等），可以将**应用打包**成可执行的JAR文件，并**直接运行**。无需额外配置独立的Servlet容器，部署和运行变得更加简单。
4. **监控和管理：**
    - 传统方式：传统Spring应用程序可能需要**手动集成监控和管理功能**，或者使用第三方工具来实现。
    - Spring Boot：Spring Boot提供了Actuator模块，可以轻松地监控和管理应用程序。通过Actuator端点，开发者可以实时监控应用的运行状态、健康状况和配置信息。
- **总结**
1. 传统方式构建Spring应用程序通常需要手动配置和整合Spring框架的各个子项目（如Spring Core、Spring MVC、Spring Data等），然后再结合其他技术（如Servlet容器、数据访问技术、安全性框架等）一起构建应用程序。
2. 而使用Spring Boot，**你只需要依赖于Spring Boot这一个框架**，Spring Boot会自动配置和整合Spring框架的各个子项目以及其他相关的技术。开发者只需提供一些基本的配置，Spring Boot就能够根据约定大于配置的原则自动配置所需的组件，大大简化了开发过程。
因此，使用Spring Boot构建Spring应用程序时，**不再需要手动整合各个子项目，而是只需关注应用程序的业务逻辑**，通过Spring Boot提供的自动配置功能快速搭建应用程序。这使得Spring Boot成为了构建Spring应用程序的首选框架之一。
#### xml（传统）和javaconfig（springboot）
- Spring Boot 则提供了一种基于注解的简化配置方式，即 JavaConfig。使用 JavaConfig 可以使用纯 Java 代码来配置 Spring 容器，无需编写 XML 配置文件。
- **使用 JavaConfig 的优势:**
	- **更加面向对象:** 可以使用 Java 代码的特性，例如继承、重用和依赖注入，来配置 Spring 容器。
	- **代码更简洁:** 可以将配置逻辑与应用程序代码放在一起，使代码更加清晰易懂。
	- **易于测试:** 可以使用单元测试来测试 JavaConfig 配置类，确保配置的正确性。
- **使用 JavaConfig 的基本步骤:**
1. 创建一个 Java 类，并使用 `@Configuration` 注解标注该类。
2. 在该类中使用 Spring 提供的注解来定义 Bean 的声明、依赖关系和其他配置信息。
3. 使用 `@ComponentScan` 注解扫描指定包路径下的 JavaConfig 类，并将其注册到 Spring 容器中。
```java
@Configuration
public class AppConfig {
  @Bean
  public MyService myService() {
    return new MyServiceImpl();
  }
}
```
- `AppConfig` 类使用 `@Configuration` 注解标注，表明它是一个 JavaConfig 配置类。
- `myService()` 方法使用 `@Bean` 注解标注，声明了一个名为 `myService` 的 Bean。
- `MyServiceImpl` 是 `MyService` 接口的实现类。
### spring boot入门
1. idea有springboot构建的模板Springlnitializr（Create Spring Boot applications using the Spring lnitializr service）会自动导入springboot-stater-web起步依赖
2. 典型的 Spring Boot 项目结构
```markdown
- src
  - main
    - java
      - com.example.demo
        - DemoApplication.java
        - controller
          - HomeController.java
    - resources
      - static
      - templates
      - application.properties
  - test
    - java
      - com.example.demo
        - controller
          - HomeControllerTest.java
```
- **src/main/java：** 存放项目的 Java 源代码。
    - **com.example.demo：** 默认的包名，可以根据实际情况修改。
        - **DemoApplication.java：** Spring Boot 应用程序的入口类，通常包含 `main` 方法。
        - **controller：** 存放控制器类，处理 HTTP 请求和响应。
            - **HomeController.java：** 示例控制器类，通常包含一些简单的请求处理方法。
- **src/main/resources：** 存放项目的资源文件。
    - **static：** 存放静态资源文件，如 CSS、JavaScript、图片等。
    - **templates：** 存放模板文件，如 Thymeleaf 或 FreeMarker 模板。
    - **application.properties：** 应用程序的配置文件，用于配置应用程序的属性和行为。
- **src/test/java：** 存放项目的测试代码。
    - **com.example.demo.controller：** 控制器测试类的包。
        - **HomeControllerTest.java：** 控制器类的测试类，用于测试控制器方法的行为。
- 除了上述的结构，还会有一些额外的文件和目录，如 Maven 的 `pom.xml` 文件、项目的 `.gitignore` 文件等.
3. 因为idea中自带的maven并没有配置，所以创建项目后还需要更改一下maven位置，
	- 解决https://start.spring.io连接不上的问题
	- 修改一下serverurl为aliyun或则springboot即可
4. 创建一个控制器类处理http请求和相应
```java
package org.darkhorse.springboot.controller;  
  
import org.springframework.web.bind.annotation.RequestMapping;  
import org.springframework.web.bind.annotation.RestController;  
  
/**  
 * @author: Bruce  
 * @description: 存放控制器类，处理htttp请求和响应  
 * @date: 2024/4/9 18:04  
 */@RestController  
public class HelloController {  
    @RequestMapping("/hello")  
    public String hello(){  
        return "Hello World!";  
    }  
}
```
5. 执行application中的main方法。通过执行项目主类中的 `main` 方法，Spring Boot 应用程序会完成初始化、自动配置、内嵌 Web 服务器启动等一系列操作，最终使得整个应用程序可以正常运行并处理来自客户端（浏览器请求对应端口就可以看到写的程序了）的请求。
### springboot的配置文件
- properties格式（记住一部分即可，idea有提示）
- yml和yaml格式（格式跟博客时的配置格式一样）**这个更常用，层级更清晰。改后缀即可**
#### yaml配置信息书写和获取
- 三方技术配置信息
- 自定义配置信息
	- **格式**：值的前面必须要有空格，作为分隔符。（找到了但是为什么博客配置没生效的原因了。。。）
	- 使用空格作为缩进表示层级关系，相同的层级左侧对齐。
	- 如果配置一个键对应多个值，则用-和空格表示一个值，其他值与此同层级
	- **获取**：使用@value（"${键名}"）进行获取。（**直接写成常量调用耦合度太高，更改就要改代码，用配置的话，不用动原来的代码。**）
	- 这样太麻烦，特别是像我之前的项目需要频繁连接数据库注解每个都要写的话太麻烦。可以在类上使用 @configurationproperties(prefix="**前缀**")，**实体类的成员变量和配置文件中的键名保持一致。**
### 整合mybatis
- **传统方式和Spring Boot 整合 MyBatis 的主要区别**:
1. **配置方式：**
    - **传统方式：** 传统方式整合 MyBatis 需要手动配置 MyBatis 的 SqlSessionFactory、数据源、事务管理器等。通常需要**编写 XML 配置文件**，并且需要手动管理各个组件之间的依赖关系。
    - **Spring Boot 方式：** 使用 Spring Boot 整合 MyBatis 通常采用注解方式配置。Spring Boot 提供了自动配置功能，可以根据项目的依赖关系自动配置 MyBatis 的 SqlSessionFactory、数据源、事务管理器等。**开发者只需简单配置几行代码**，Spring Boot 就能自动完成整合，无需手动编写大量的 XML 配置文件。
2. **自动化程度：**
    - **传统方式：** 传统方式需要开发者手动配置和管理各个组件的依赖关系，可能需要**编写大量的 XML 配置文件**，并且需要处理各种细节问题。
    - **Spring Boot 方式：** Spring Boot 提供了自动配置功能，可以根据项目的依赖关系自动配置 MyBatis 相关的组件。**开发者只需提供必要的配置信息**，Spring Boot 就能自动完成整合，并且能够处理各种细节问题，大大简化了配置和部署过程。
3. **简化程度：**
    - **传统方式：** 传统方式需要开发者手动配置各个组件的依赖关系，可能需要**编写大量的 XML 配置文件**，配置繁琐，容易出错。
    - **Spring Boot 方式：** Spring Boot 提供了自动配置功能，可以根据项目的依赖关系自动配置 MyBatis 相关的组件，大大简化了配置过程。**开发者只需专注于业务逻辑的实现，无需关注过多的配置细节。**
- 总的来说，使用 Spring Boot 整合 MyBatis 相比传统方式，配置更简单、自动化程度更高，能够大大提高开发效率，降低了项目的开发和维护成本。因此，越来越多的开发者选择**使用 Spring Boot 来构建 MyBatis 集成**的应用程序。
### bean扫描
- springboot默认扫描启动类所在的包以及子包
- 要指定以外的包需要在启动类上添加@ComponentScan(basePackages = "包名")
- 一般开发都写在这个启动类所在的包
### bean注册
- `@Component`：是 Spring 中最常用的 Bean 注册注解，可以用于注册任何类型的 Bean。
- `@Service`：用于注册服务层 Bean，通常用于处理业务逻辑。
- `@Repository`：用于注册数据访问层 Bean，通常用于访问数据库。（由于与mybatis整合用的少）
- `@Controller`：用于注册 Web 层 Bean，通常用于处理 Web 请求。
- **如果要注册的对象来自第三方（不是自定义的），无法使用以上四个注解**
- 解决方案：
#### @bean
1. 在 Spring Boot 的启动类或配置类中使用 `@Bean` 注解来注册第三方 Bean。
2. `@Bean` 注解可以用于注册任何类型的 Bean，包括来自第三方的 Bean。
3. 要注册多个第三方 Bean，建议在配置类中集中注册
4. **集中注册第三方 Bean 的优势:**
- **代码更简洁:** 可以将所有第三方 Bean 的注册集中在一个地方，使代码更加简洁易懂。
- **易于维护:** 可以集中管理所有第三方 Bean 的注册，方便维护和更新。
- **避免冲突:** 可以避免不同类中注册的第三方 Bean 发生冲突。
- 步骤：
	- 创建一个专门的配置类来注册第三方 Bean。
	- 使用 `@Bean` 注解在配置类中注册第三方 Bean。
	- 使用 `@Import` 注解导入其他配置类，该配置类中包含了需要注册的第三方 Bean（在启动类中则不需要使用 `@Import` 注解显式导入）
```java
//启动类
@SpringBootApplication
public class App {
  public static void main(String[] args) {
    SpringApplication.run(App.class, args);
  }
  //导入其他配置类
  @Import(MyConfig.class)
  public void config() {
  }
}
//配置类，专门用于注册第三方bean对象
@Configuration
public class MyConfig {
  @Bean
  public MyService myService() {
    return new MyServiceImpl();
  }
  @Bean
  public MyOtherService myOtherService() {
    return new MyOtherServiceImpl();
  }

}

public class MyService {
  public void doSomething() {
    // ...
  }
}

public class MyServiceImpl implements MyService {
  @Override
  public void doSomething() {
    // ...
  }
}

public class MyOtherService {
  public void doSomethingElse() {
    // ...
  }
}

public class MyOtherServiceImpl implements MyOtherService {
  @Override
  public void doSomethingElse() {
    // ...
  }
}
```
在这个示例中，我们创建了 `MyConfig` 配置类来集中注册 `MyService` 和 `MyOtherService` 两个第三方 Bean。在 `App` 类中的 `config` 方法上使用了 `@Import(MyConfig.class)` 注解，这意味着在 Spring Boot 应用程序启动时，会将 `MyConfig` 配置类中定义的 Bean 注册到 Spring 容器中。
- bean对象默认的名字为方法名，直接在注释中指定：@bean("名字")
- 如果方法内部需要使用到ioc容器中已经存在的bean对象，那么只需要在方法形参中声明即可，spring会自动注入
#### @import
- 不在启动类中，需要显示导入。
- 一次性导入多个配置类：导入importselect接口实现类
	1. 如果要在启动类中一次性导入多个配置类，可以使用 `@Import` 注解结合 `MyImportSelector` 类。`MyImportSelector` 类实现了 `ImportSelector` 接口，它可以动态地选择要导入的配置类，根据条件来确定要导入的配置类列表。
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Import;
import org.springframework.context.annotation.ImportSelector;
import org.springframework.core.type.AnnotationMetadata;

@SpringBootApplication
@Import(MyImportSelector.class)
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}

class MyImportSelector implements ImportSelector {
    @Override
    public String[] selectImports(AnnotationMetadata annotationMetadata) {
        // 返回需要导入的配置类的全限定类名数组
        //如果很多，可以写到一个文件中，直接读取文件即可
        return new String[] {"com.example.Config1", "com.example.Config2"};
    }
}
```
#### 组合注解
- 可以使用组合注解来简化配置，提高代码的可读性和美观性。组合注解是将多个注解组合在一起，形成一个新的注解，这样在使用时只需要使用这个组合注解，就相当于使用了其中的所有注解。
#### 注册条件
- 场景：在方法中形参获取配置文件中的值，但是配置文件并没设置相关的值。那么这时为了不报错，配置了就用配置的值，没配置就不注册（不然你用@value去获取，但是又没有配置会报错）
- **`@ConditionalOnProperty`**：当指定的属性设置为指定的值时，才会创建 Bean。
可以使用 `prefix` 和 `name` 参数来指定属性的前缀和键名，而不指定具体的属性值。这样做可以在配置文件中设置具体的属性值，并且只要存在以指定前缀开头的属性，就会创建 Bean。
```java
import org.springframework.boot.autoconfigure.condition.ConditionalOnProperty;
import org.springframework.stereotype.Service;

@Service
@ConditionalOnProperty(prefix = "myapp.service", name = "enabled")
public class MyService {
    public void doSomething() {
        System.out.println("MyService is doing something...");
    }
}
```
使用了 `prefix` 参数指定了属性的前缀为 `"myapp.service"`，而 `name` 参数指定了属性的键名为 `"enabled"`。这样，只要在配置文件中存在以 `"myapp.service.enabled"` 开头的属性，不论其具体值是什么，都会创建 `MyService` Bean。
- **`@ConditionalOnMissingBean`**：当bean容器中不存在指定的 Bean 时，才会创建当前 Bean。
```java
import org.springframework.boot.autoconfigure.condition.ConditionalOnMissingBean;
import org.springframework.stereotype.Service;

@Service
@ConditionalOnMissingBean(MyService.class)
public class MyService {
    public void doSomething() {
        System.out.println("MyService is doing something...");
    }
}

```
- `@ConditionalOnClass`：当类路径中存在指定的类时，才会创建 Bean。
```java
import org.slf4j.Logger;
import org.springframework.boot.autoconfigure.condition.ConditionalOnClass;
import org.springframework.stereotype.Service;

@Service
@ConditionalOnClass(Logger.class)
public class MyService {
    public void doSomething() {
        System.out.println("MyService is doing something...");
    }
}
```
在这个示例中，`MyService` 类上添加了 `@ConditionalOnClass` 注解。这个注解指定了一个参数：
- `value`：指定了要检查的类，这里是 `Logger.class`。意味着只有当类路径中存在 `org.slf4j.Logger` 类时，才会创建当前 Bean。
现在，如果类路径中存在 `org.slf4j.Logger` 类，则会创建 `MyService` Bean。如果类路径中不存在这个类，则不会创建这个 Bean。
### 自动配置原理
所谓自动配置，不过是别人封装好的手动配置而已。
### 自定义starter
- 自定义 Starter 的应用场景是在需要在多个项目中复用通用功能、解决方案、最佳实践或集成第三方服务时。通过将这些功能封装成 Starter，可以提高代码的复用性、可维护性和可扩展性，减少重复劳动，并且使项目的开发过程更加高效和规范。
- 如spring-boot-starter-web，spring-boot-starter-test
- **如果本地仓库中有的话，在引入依赖时可以先从artifactId标签开始写会有提示。**
