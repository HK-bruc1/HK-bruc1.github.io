---
title: Spring6
date: 2024-03-23T12:01:31+08:00
lastmod: 2024-03-31
draft: false
image: cover.jpg
description: 之前文章太长了新开一篇不然软件有一点卡
keywords: spring6
tags:
  - java
  - spring
categories:
  - 工作
slug: 0810724b
---
## Spring Boot / Spring MVC
- Spring框架核心：在学习Spring Boot和Spring MVC之前，建议先学习Spring框架的核心概念，包括控制反转（IoC）、依赖注入（DI）、面向切面编程（AOP）等。这些概念是Spring Boot和Spring MVC的基础。
- Spring Boot入门：学习如何使用Spring Boot来快速构建Java应用程序。了解Spring Boot的核心特性、自动配置原理、Starter依赖等内容。
- Spring MVC基础：学习Spring MVC框架的基本概念，包括控制器、视图解析器、模型数据绑定等。理解MVC架构的基本原理以及如何在Spring MVC中实现。
- Spring Boot与Spring MVC集成：学习如何在Spring Boot应用程序中集成Spring MVC，以及如何利用Spring Boot的自动配置简化Spring MVC应用程序的开发和部署。
### spring6
- 创建一个空工程后需要设置一下jdk版本，需要maven来管理依赖，所以也要设置一下。
- OCP 原则的核心思想是：
	- 开放性（Open for Extension）：软件实体（类、模块、函数等）应该对扩展是开放的。这意味着可以在**不修改现有代码的情况下添加新功能或行为。**
	- 封闭性（Closed for Modification）：软件实体应该对修改是封闭的。**这意味着已经存在的代码不应该被修改**，因为**任何修改可能会导致不必要的风险和影响现有功能的稳定性**。
	- 实现 OCP 原则的一种常见方法是使用**抽象和多态**。通过定义抽象接口和基类，可以在不修改现有代码的情况下引入新的实现。这样一来，**新的功能可以通过实现现有的抽象接口来添加，而无需修改现有的代码。**
- 依赖倒置原则（Dependency Inversion Principle，简称DIP）是面向对象设计中的一个重要原则，由罗伯特·马丁（Robert C. Martin）提出。该原则的核心思想是：
	- 高层模块不应该依赖于底层模块。两者都应该依赖于抽象（**底层一动导致调用它的高层也要相应修改**）。
	- 抽象不应该依赖于具体实现。具体实现应该依赖于抽象（**抽象类中定义了方法的抽象接口，而具体的实现类负责实现这些方法。这样一来，抽象类就不依赖于具体实现，而是由具体实现来依赖抽象**）。
	- 换句话说，依赖倒置原则要求在设计软件系统时，应该针对抽象编程，而不是针对具体实现编程。这样可以降低模块之间的耦合度，提高代码的灵活性、可维护性和可扩展性。
	- **我确实用了接口，也用了A类来实现接口中的抽象方法，那我B类调用这个A类时，new的是A的类名。那我扩展功能时，重新创建一个C类来实现接口，导致B类需要更改。**
	- 在某些情况下，**即使你使用了接口和抽象类**，但如果**在实际使用中依然需要直接实例化具体的实现类**，那么确实会违背依赖倒置原则。
	- 不new具体实现类即可以达到耦合度大大降低，但是null空指针异常，可以使用**控制反转**思想解决这个问题。
- 控制反转（Inversion of Control，IoC）是一种软件设计思想（新的设计模式），可以帮助解决依赖倒置原则中的问题，并且有助于降低代码耦合度。
	- 控制反转的核心思想是将**对象的创建和管理交给外部容器来负责**，而不是在应用程序中硬编码。通常，这个容器被称为 IoC 容器。通过使用 IoC 容器，可以实现依赖对象的自动注入，从而避免了手动创建和管理对象之间的关系。
- 所以spring框架孕育而出，Spring 框架可以说是控制反转和依赖注入思想的**典型实现之一**。Spring 框架提供了一个容器，称为 Spring IoC 容器，用于**管理应用程序中的对象及其之间的依赖关系**。Spring IoC 容器负责对象的创建、初始化、注入依赖等工作，从而实现了控制反转和依赖注入。控制反转强调的是将对象的控制权转移给外部容器，而依赖注入是实现控制反转的一种具体方式。Spring 框架是控制反转和依赖注入**思想**的典型实现
- 通过依赖注入，可以将**依赖的对象注入到目标对象中**，从而实现了对象之间的解耦和管理。依赖注入（Dependency Injection，DI）常见的两种实现方法是构造函数注入（Constructor Injection）和属性注入（Setter Injection）
	- 构造函数注入（构造方法给属性赋值）是通过类的构造函数来注入依赖的方式。具体来说，就是在类的构造函数中**接收依赖对象作为参数**，并将其赋值给类的成员变量。通常，依赖对象会在类实例化的时候通过构造函数传入，然后在类的内部使用这些依赖对象。
	- 属性注入（用setter方法给属性赋值）是通过类的属性（成员变量）来注入依赖的方式。具体来说，就是通过类的 setter 方法将依赖对象注入到类的属性中。通常，依赖对象会在类实例化后通过 setter 方法来设置。
	- 依赖：A对象与B对象的关系
	- 注入：是一种手段，同过这一手段使A对象和B对象产生关系
- 引入spring的基础依赖（spring-context以及相关的依赖）使用maven更便捷
```Java
<dependencies>  
    <dependency>  
        <groupId>org.springframework</groupId>  
        <artifactId>spring-context</artifactId>  
        <version>6.1.4</version>  
    </dependency>  
</dependencies>
```
- 使用bean管理对象，需要配置spring的相关文件（在resource文件中，idae有模板）
	- bean两个重要标签一个是id（唯一标识）一个是class（带包名的全路径）
	- `<bean id="userBean" class="bean.User"/>`
- 使用bean：
	- `ApplicationContext context = new ClassPathXmlApplicationContext("firstSpring.xml");`
	- 这段代码创建了一个 Spring 应用程序上下文（ApplicationContext）对象，并加载了一个名为 "firstSpring.xml" 的 XML 配置文件。让我逐步解释这段代码：ApplicationContext context: 这一行声明了一个名为 context 的变量，它将保存 Spring 应用程序上下文对象的引用。new ClassPathXmlApplicationContext("firstSpring.xml"): 这部分代码创建了一个 ClassPathXmlApplicationContext 对象，**它是 ApplicationContext 接口的一个实现类**。ClassPathXmlApplicationContext 类用于**从类路径加载 XML 配置文件，并根据这些配置文件创建 Spring 容器**。在这里，通过传递 "firstSpring.xml" 字符串作为参数，告诉 Spring 容器加载名为 "firstSpring.xml" 的配置文件。"firstSpring.xml": 这是 XML 配置文件的名称。XML 配置文件通常包含了 Spring 应用程序的组件定义，比如 bean 的配置、依赖注入等等。在这个例子中，"firstSpring.xml" 文件将包含至少一个 bean 的定义。
	- 总结为两步：
		- 获取spring容器对象
		- 根据bean的id从容器中获取这个对象
	- 总的来说，这段代码的作用是**创建一个 Spring 容器，并根据指定的 XML 配置文件加载和初始化该容器，从而使得在这个容器中定义的 bean 可以被实例化和管理**。
- 在默认情况下，如果你没有提供显式的构造函数，并且你的类中包含了一个无参构造函数（系统提供的），Spring 将会使用该无参构造函数来创建对象。这是因为 Java 在没有显式定义构造函数时会提供一个默认的无参构造函数。那么当你在 Spring 的 XML 配置文件中声明该类的 bean 时，Spring 将使用这个无参构造函数来创建对象，**在这种情况下，Spring 会使用无参构造函数来实例化对象。这是 Spring 对于对象实例化的默认行为**。
- 通常情况下，Spring 容器会根据配置文件中的声明**实例化所有的 bean**，并根据需要对其进行依赖注入。当你需要使用某个 bean 时，你可以从 Spring 容器中获取该 bean 的实例。
- 在内部，Spring 容器一般使用 Map 或类似的数据结构来存储 bean 的实例，**以 bean 的 ID 或名称作为键，bean 实例作为值**。这样，当你通过 bean 的 ID 或名称请求某个 bean 时，Spring 容器可以快速地将相应的 bean 实例返回给你。
- 如果bean的id不存在，会报错。
#### 依赖注入之set
- 想要spring调用对应的set注入方法，需要在spring配置文件中对应的bean标签中设置property，name属性值（**指向的是set方法**）：**set方法的方法名**，去掉set，余下首字母小写。ref指的是要注入的bean的id，从而建立起两个bean的关系。直接用idea生成的set方法即可。
- **效果：对象交给bean之后，如果是相同结构不同实现的话（替换），只需要改spring的配置即可。（新增功能就可以直接增加代码而不改动原有代码）**
#### 依赖注入之构造方法
```xml
<bean id="MySQL" class="com.powernode.spring6.dao.impl.UserDaoImplForMySQL"/>  
<bean id="UserServiceBean" class="com.powernode.spring6.service.impl.UserServiceImpl">  
    <constructor-arg index="0" ref="MySQL"/>  
</bean>
```
- 仅仅是在配置配置上的不同而异。也可以用**构造函数的参数的名字**
#### set注入专题
- 声明bean和内部bean以及外部bean
- 主要是外部bean的写法
```xml
<!-- 内部 bean 方式 --> 
<bean id="externalBean" class="com.example.ExternalBean"> 
<property name="internalBean"> 
<bean class="com.example.InternalBean"/> 
</property> 
</bean>
<!-- 外部 bean 注入方式 --> 
<bean id="externalBean" class="com.example.ExternalBean"> 
<property name="internalBean" ref="internalBean"/> </bean>
<!-- 声明bean --> 
<bean id="internalBean" class="com.example.InternalBean"/>
```
- Spring 可以使用 set 注入给简单类型赋值。简单类型包括基本数据类型（如 int、float、double 等）以及其对应的包装类型（如 Integer、Float、Double 等）以及 String 等。
```xml
<!-- 定义一个名为 "exampleBean" 的 bean --> 
<bean id="exampleBean" class="com.example.ExampleBean"> 
<!-- 使用 set 方法注入属性值 --> 
<property name="name" value="John"/> 
<property name="age" value="30"/> 
</bean>
```
- 然后，在 `ExampleBean` 类中，你需要提供对应的属性，并提供相应的 setter 方法来允许 Spring 进行属性注入
- 这又是何苦？都可以用spring创建对象了，等获取bean对象后直接使用set方法不是不是直观一点？
- **当你已经获取了 Spring 容器中的 bean 对象后，直接使用对象的 setter 方法来设置属性值是一种更直观的方式。这种方式也是很常见的，并且在实际项目中被广泛使用。**
- 一种常见的做法是结合使用两种方式：
	1. 在配置文件中设置一些默认值或者初始值，以便在需要时能够方便地修改配置。
	2. 在代码中使用 setter 方法根据需要覆盖配置文件中的值，以满足特定的业务需求。
这样既能够充分利用 Spring 的依赖注入特性，又能够保持代码的可读性和可维护性。
- 简单类型经典应用：一个经典的应用场景是在配置类中注入简单类型的属性，例如配置数据库连接信息、端口号等。通过这种方式，我们可以将简单类型的属性值从外部配置文件中注入到 Spring 管理的 bean 中，实现了配置与代码的分离，使得配置更加灵活和易于维护
- 注入数组
```Java
public class DataProcessor {
    private String[] data;

    public void setData(String[] data) {
        this.data = data;
    }
}
```
在 Spring 配置文件中，我们可以通过 `<property>` 元素将数组注入到 `DataProcessor` 类中：
```xml
    <bean id="dataProcessor" class="com.example.DataProcessor">
        <property name="data">
            <array>
                <value>Item 1</value>
                <value>Item 2</value>
                <value>Item 3</value>
            </array>
        </property>
    </bean>
```
- 注入list集合和Set集合
```java
import java.util.List;
import java.util.Set;

public class User {
    private List<String> rolesList;
    private Set<String> rolesSet;

    public void setRolesList(List<String> rolesList) {
        this.rolesList = rolesList;
    }

    public void setRolesSet(Set<String> rolesSet) {
        this.rolesSet = rolesSet;
    }
}
```
在 Spring 的配置文件中，我们可以使用 `<list>` 和 `<set>` 元素来分别注入 List 和 Set 集合：
```xml
    <bean id="user" class="com.example.User">
        <property name="rolesList">
            <list>
                <value>ROLE_USER</value>
                <value>ROLE_ADMIN</value>
            </list>
        </property>
        <property name="rolesSet">
            <set>
                <value>ROLE_USER</value>
                <value>ROLE_ADMIN</value>
            </set>
        </property>
    </bean>
```
list集合有序可重复，set集合无序不可重复。简单类型和非简单类型的区别就是一个用value和ref
- 注入Map
```Java
import java.util.Map;
public class User {
    private Map<String, String> rolesMap;

    public void setRolesMap(Map<String, String> rolesMap) {
        this.rolesMap = rolesMap;
    }
}
```
在 Spring 的配置文件中，我们可以使用 `<map>` 元素来定义 Map，并使用 `<entry>` 元素来添加键值对：
```xml
    <bean id="user" class="com.example.User">
        <property name="rolesMap">
            <map>
                <entry key="ROLE_USER" value="User Role"/>
                <entry key="ROLE_ADMIN" value="Admin Role"/>
            </map>
        </property>
    </bean>
```
- 不给属性注入默认注入null（不是注入字符串"null"）
- 手动给属性赋空值：
```Java
public class User {
    private String email;

    public void setEmail(String email) {
        this.email = email;
    }
}
```
然后，在 Spring 的配置文件中，我们可以使用 `<null>` 元素来注入 null 值：
```xml
    <bean id="user" class="com.example.User">
        <property name="email">
            <null/>
        </property>
    </bean>

```
- 注入的值中含有特殊字符（两种方案）
```xml
    <!-- 使用实体符号 -->
    <bean id="user1" class="com.example.User">
        <property name="description" value="User &amp; Example"/>
    </bean>

    <!-- 使用CDATA区块 -->
    <bean id="user2" class="com.example.User">
        <property name="description">
            <![CDATA[User < Example]]>
        </property>
    </bean>
```
- P命名空间（基于set方法）：
```Java
public class User {
    private String name;
    private Address address;

    // getter 和 setter 方法
}

public class Address {
    private String city;
    private int zipcode;

    // getter 和 setter 方法
}
```
配置 Spring XML 文件，使用 P 命名空间注入这些属性的值：
```
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:p="http://www.springframework.org/schema/p"
    <!-- 注入简单类型属性值 -->
    <bean id="user" class="com.example.User" p:name="John"/>

    <!-- 注入非简单类型属性值 -->
    <bean id="address" class="com.example.Address" p:city="New York" p:zipcode="12345"/>
    <bean id="userWithAddress" class="com.example.User" p:name="Jane" p:address-ref="address"/>
</beans>
```
- C命令空间（基于构造方法）：
```Java
public class User {
    private String name;
    private int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```
使用 C 命名空间在 Spring 配置文件中执行构造方法注入：
```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:c="http://www.springframework.org/schema/c"
    <bean id="user" class="com.example.User" c:_0="John" c:_1="30"/>
</beans>
```
`c:_0` 和 `c:_1` 分别代表构造函数的第一个和第二个参数。
在实际的开发中，使用 P（Property）和 C（Constructor）命名空间来进行属性注入确实是一种简化配置的常见做法。这两种命名空间可以使配置文件更加简洁、易读，并且减少了不必要的模板代码。因此，它们在实际项目中被广泛应用。
- 使用util命名空间
```xml
       xmlns:util="http://www.springframework.org/schema/util"
       http://www.springframework.org/schema/util/spring-util.xsd">
    <!-- 共享的数据库连接属性配置 -->
    <util:properties id="dbProperties">
        <prop key="driverClassName">com.mysql.jdbc.Driver</prop>
        <prop key="url">jdbc:mysql://localhost:3306/example</prop>
        <prop key="username">root</prop>
        <prop key="password">password</prop>
    </util:properties>

    <!-- 数据源1 -->
    <bean id="dataSource1" class="org.apache.commons.dbcp2.BasicDataSource">
        <property name="driverClassName" ref="dbProperties"/>
    </bean>

    <!-- 数据源2 -->
    <bean id="dataSource2" class="org.apache.commons.dbcp2.BasicDataSource">
        <property name="driverClassName" ref="dbProperties"/>
    </bean>
</beans>
```
- **按名称（byName）**：Spring 会自动在容器中查找与 bean 属性名相同的 bean，并将其注入到相应的属性中。这种模式可以用于 setter 方法注入和构造函数注入（死活不行）。
```xml
    <!-- 设置注入示例 -->
    <bean id="student" class="com.example.Student">
        <property name="name" value="Alice" />
        <property name="age" value="20" />
    </bean>

    <!-- Bean注入到另一个Bean中示例 -->
    <bean id="teacher" class="com.example.Teacher">
        <property name="student" ref="student" />
    </bean>
    
    <!-- 设置注入示例，指定byName自动装配，在类中使用set注入 --> 
    <bean id="teacher" class="com.example.Teacher"autowire="byName"/>     <!-- Bean注入到另一个Bean中示例，id应该为Teacher中的set方法参数名 --> 
    <bean id="student" class="com.example.Student" />
```
- **构造函数（constructor）**：Spring 会自动根据构造函数参数的类型在容器中查找相应的 bean，并将其注入到构造函数中。这种模式只能用于构造函数注入，不能用于 setter 方法注入。autowire="constructor"
- **按类型（byType）**：Spring 会自动在容器中查找与 bean 属性类型相同的 bean，并将其注入到相应的属性中。**这种模式只能用于 setter 方法注入**，不能用于构造函数注入。（bean的id都不需要，但缺点是同类型实例bean不能有多个）
#### 引入外部的属性配置文件
- jdbc.properties文件需要导入到配置文件中：
```properties
jdbc.driverClass=com.mysql.cj.jdbc.Driver  
jdbc.url=jdbc:mqsql://localhost:3306/spring6  
jdbc.username=root  
jdbc.password=123
```
- 在相关类中定义对应接收变量并对外提供set方法
- xml配置文件
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xmlns:context="http://www.springframework.org/schema/context"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd  
       http://www.springframework.org/schema/context  http://www.springframework.org/schema/context/spring-context.xsd">  
  
    <!-- 引入外部的properties文件 -->  
    <!--    xmlns:context="http://www.springframework.org/schema/context" -->    <!--http://www.springframework.org/schema/context  http://www.springframework.org/schema/context/spring-context.xsd-->    <!-- 1.引入context命名空间 -->  
    <!-- 2.使用context:property-placeholder的location属性指定，默认从类的根路径（resource）下加载资源 -->  
    <context:property-placeholder location="jdbc.properties"/>  
    <bean id="ds" class="com.powernode.spring6.jdbc.MyDataSource">  
        <!-- 3.取值：用${key}用带前缀的命名防止取到系统变量 -->  
        <property name="driver" value="${jdbc.driverClass}"/>  
        <property name="url" value="${jdbc.url}"/>  
        <property name="username" value="${jdbc.username}"/>  
        <property name="password" value="${jdbc.password}"/>  
    </bean>  
</beans>
```
#### bean作用域之单例和多例
- spring默认情况下是如何管理bean的？
在spring上下文初始化时实例化，每一次调用getBean（）都是返回那个单例的对象
- 通过spring的配置文件的bean标签设置，scope为prototype,那么每一次调用getBean（）都会实例化一个对象。（在上下文初始化时并不会实例化对象）
- **request**：每个 HTTP 请求都会创建一个新的 bean 实例，该 bean 实例仅在当前 HTTP 请求范围内有效。适用于 Web 应用中，确保每个 HTTP 请求都有自己的独立实例。
- **session**：每个 HTTP 会话（Session）都会创建一个新的 bean 实例，该 bean 实例仅在当前会话范围内有效。适用于 Web 应用中，确保每个用户会话都有自己的独立实例。
- **application**：整个 Web 应用中都共享同一个 bean 实例，该 bean 实例在应用启动时创建，并在应用关闭时销毁。适用于 Web 应用中需要共享的全局资源。
- **websocket**：每个 WebSocket 连接都会创建一个新的 bean 实例，该 bean 实例仅在当前 WebSocket 连接范围内有效。适用于使用 WebSocket 技术的 Web 应用中，确保每个 WebSocket 连接都有自己的独立实例。
- **custom**：自定义作用域，您可以通过实现 `org.springframework.beans.factory.config.Scope` 接口来定义自己的作用域。这种方式允许您根据特定需求定义更灵活的作用域。
- 还可以自定义bean的scope（比如一个线程一个bean...）
#### 简单工厂模式
- 简单工厂模式主要解决了**对象的创建过程与客户端代码之间的耦合问题**
	- **隐藏对象创建细节：** 简单工厂模式将对象的创建过程封装在工厂类中，客户端**无需知道具体的创建细节**，只需要**通过工厂类来获取**所需的对象。这样可以隐藏对象创建的复杂性，使客户端代码更加简洁。
	- **集中控制对象创建：** 通过工厂类**集中控制对象的创建**，可以在需要时方便地对创建过程进行修改和扩展，而不需要修改客户端代码。这种集中控制的方式有利于系统的维护和管理。
	- **降低客户端与具体产品类之间的耦合度：** 客户端**只依赖于工厂类**而不依赖于具体的产品类，这样可以降低客户端与具体产品类之间的耦合度。如果需要**替换产品类**，**只需要修改工厂类的代码**即可，不会影响到客户端代码（违背了OCP原则）
	- **统一管理产品对象：** 通过**工厂类统一管理产品对象的创建**（不能出问题，运行起来不要轻易修改），可以确保对象的一致性和合法性。工厂类可以根据一定的逻辑来创建对象，保证对象的状态和行为符合设计要求。
- 简单工厂的角色
	- 抽象产品角色（抽象武器父类）
	- 具体产品角色（子类具体武器继承父类重写抽象方法）
	- 工厂类角色（定义一个静态方法实现对武器对象的获取，在客户端只需要调用这个方法即可获取对象，调用对象的方法而不需要关心对象是如何创建的）
- 缺点1：扩展一个新的武器，那么工厂类的代码是需要修改的（提供对武器对象创建的实现），违背了OCP原则
- 缺点2：工厂类的责任太重，不能出现任何问题，因为工厂负责所有产品的生产，称为全能类，一旦出现问题，整个系统就会瘫痪。
#### 工厂方法模式（解决OCP问题）
- 一个工厂对应一个武器产品
- 加产品对应加工厂就可以了。不用修改原来代码。（添加两个类即可）
- 工厂方法模式中的角色
	- 抽象产品
	- 具体产品
	- 抽象工厂（创建实例方法，为了使用工厂准备）
	- 具体工厂（一个具体产品对应一个具体工厂）
- 缺点
	- 每增加一个产品，就要增加两个类（需要new两个对象，开销太大），使系统中的类数量增多
	- 增加了系统的复杂度，同时增加了具体类的依赖。
#### bean的获取的四种方式
1. **构造函数实例化（Constructor Injection）：**
    - 使用构造函数注入的方式来实例化 Bean。通过在 Bean 的类中定义带有参数的构造函数，并在 Spring 配置文件中指定构造函数参数的值，Spring 容器会根据配置使用相应的构造函数来实例化 Bean。
2. **静态工厂方法实例化（Static Factory Method 简单工厂模式）：**
    - 使用静态工厂方法来创建 Bean。在 Bean 的类中定义一个静态方法，通过该静态方法来创建 Bean 的实例。在 Spring 配置文件中通过 `<bean>` 元素的 `factory-method` 属性指定静态工厂方法的名称，Spring 容器会调用该方法来创建 Bean 的实例。
3. **实例工厂方法实例化（Instance Factory Method）：**
    - 使用实例工厂方法来创建 Bean。在一个普通的类中定义一个实例方法，通过该实例方法来创建 Bean 的实例。在 Spring 配置文件中通过 `<bean>` 元素的 `factory-bean` 和 `factory-method` 属性指定实例工厂方法所在的 Bean 的名称和方法名，Spring 容器会调用该实例方法来创建 Bean 的实例。
4. **工厂Bean实例化（FactoryBean）：**
    - 使用实现了 `FactoryBean` 接口的工厂 Bean 来创建 Bean。`FactoryBean` 接口是 Spring 框架提供的一个接口，定义了一个方法用于返回创建的 Bean 实例。通过实现 `FactoryBean` 接口并实现其中的 `getObject()` 方法，可以自定义 Bean 的创建过程。在 Spring 配置文件中通过 `<bean>` 元素的 `class` 属性指定工厂 Bean 的类名，Spring 容器会调用工厂 Bean 的 `getObject()` 方法来获取创建的 Bean 实例。
- 通过简单工厂实例化bean
	- **应该先查看对应的 `<bean>` 标签中的 `class` 属性确定 Bean 的类型，然后根据具体情况来决定如何填入 `context.getBean()` 方法的第二个参数。**
	- spring配置（告诉spring在get方法中获取bean）
	- `<bean id="Factory" class="BeanFactory" factory-method="get"/>`
	- 定义一个star类提供无参构造方法
	- 再定义一个工厂类提供一个返回值为star的静态方法get(),在方法体中直接返回new star()  **相当于自己new了。。。**
	- 在测试类中
```Java
ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml");  
Star star = context.getBean("Factory",Star.class);  
System.out.println(star);
```
如果你在 Spring 容器中声明的 Bean 名称为 "Factory"，并且类为 "BeanFactory"，但你希望获取的实际 Bean 类型为 "Star"，那么可能有两种情况：
- **BeanFactory 中的 get 方法返回的是 Star 类型的实例**
如果在 BeanFactory 中的 get 方法确实返回了 Star 类型的实例，那么 Spring 容器将根据 `Star.class` 指定的类型来匹配实际的 Bean 实例。
- **使用工厂方法来创建 Star 类型的 Bean**
如果 BeanFactory 是一个工厂类，它的 `get()` 方法并不直接返回一个 Star 类型的实例，而是**用来创建 Star 类型的实例**，则需要在 Spring 配置文件中配置一个 FactoryBean 来指定如何创建 Star 类型的 Bean。
- **静态工厂方法实例化使用背景**：
1. **创建逻辑复杂：** 当对象的创建逻辑比较复杂，可能涉及到多个步骤或者依赖关系时，使用工厂类可以将对象的创建过程封装起来，使客户端代码更加简洁和易于维护。
2. **对象的创建方式不固定：** 如果对象的创建方式可能会根据不同的条件或者策略而变化，使用工厂类可以根据具体的情况来动态地选择合适的创建方式，而不需要修改客户端代码。
3. **降低耦合度：** 工厂类将对象的创建过程与客户端代码解耦，客户端无需了解具体的创建细节，只需要通过工厂类来获取所需的对象，从而降低了客户端与具体产品类之间的耦合度。
4. **统一管理对象的创建：** 使用工厂类可以集中管理对象的创建过程，便于维护和管理，同时可以确保对象的一致性和合法性。
5. **提供灵活性和可扩展性：** 工厂类可以根据需要动态地创建不同类型的对象，可以方便地扩展和修改对象的创建逻辑，从而提供了更大的灵活性和可扩展性。
- **实例工厂方法实例化（Instance Factory Method）**
spring配置：
```xml
<bean id="TankBean" class="TankFactory"/>  
告诉spring调用那个对象以及对象的的那个方法
<bean id="tank" factory-bean="TankBean" factory-method="get"/>
```
类中的方法改为实例方法即可。获取tank的bean对象即可完成tank()对象初始化。
- **工厂Bean实例化（FactoryBean）** 实际上为第三种的简化
tan类给一个无参构造。tankfactory类实现FactoryBean接口，重写其中的方法，在配置中即不需要指定factory-bean和factory-method。只需要定义一个bean对象即可。重写的方法中new tank（）还是自己写到getObject()方法中。
- `FactoryBean` 是一个接口，用于定义一个工厂 Bean，它负责创建其它 Bean 实例。
- `BeanFactory` 是 Spring IoC 容器的顶层接口，负责管理 Bean 的生命周期和依赖关系。
`FactoryBean` 主要用于创建复杂的 Bean 实例，而 `BeanFactory` 主要用于管理 Bean 实例的生命周期和依赖关系。
#### bean的生命周期之五步
1. 实例化bean（调用无参构造方法）
2. bean属性赋值（调用set方法）
3. **初始化bean（调用init方法，这个ini需要自己写，自己配）**
4. 使用bean
5. 销毁bean（会调用destory方法，方法自己写，自己配）
- 总的来说，**无参构造方法**用于**实例化Bean对象**，而**setter方法和有参构造方法**则用于**设置Bean的属性值或进行构造方法注入**。这些步骤之间的具体顺序可以根据Bean的定义和依赖关系而有所不同。通常情况下，**实例化Bean对象是第一步，然后是属性设置或构造方法注入**，最后是其他依赖的初始化和注入。
- 当Spring容器实例化Bean对象（调用无参构造方法）时，会根据配置文件中的定义，通过setter方法或有参构造方法将这些属性的值注入到Bean对象中。
- 通常情况下，在**使用有参构造方法注入依赖时**，**建议同时提供一个无参构造方法**。这是因为当Spring容器实例化Bean对象时，默认会使用无参构造方法来创建对象。如果Bean类中只提供了有参构造方法而没有提供无参构造方法，Spring容器会尝试使用默认的无参构造方法来实例化对象，但由于没有默认的无参构造方法可用，实例化过程会失败，导致Bean无法被正确地创建
- **无参构造是用来创建bean容器的，如果要按照配置中的值来初始化bean对象属性值那么必须要提供一种注入方式**
- 初始化bean和销毁bean，方法需要自己写并在xml配置中指明init-method="" destroy-method=""。
```Java
ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml"); 
// 执行应用程序逻辑 
// 当应用程序结束时，手动关闭应用程序上下文 ((ClassPathXmlApplicationContext) context).close();
```
#### bean的生命周期之七步
1. 实例化bean
2. bean属性赋值
3. **执行“bean后处理器”的before方法**
4. 初始化bean
5. **执行“bean后处理器”的after方法**
6. 使用bean
7. 销毁bean
- **执行“Bean后处理器”的before方法**：如果有配置了Bean后处理器（BeanPostProcessor），Spring容器在初始化Bean之前会先执行这些后处理器的before方法。
- **执行“Bean后处理器”的after方法**：在初始化Bean后，Spring容器会再次执行配置的Bean后处理器的after方法。
- 在Spring中编写Bean后处理器：
**创建后处理器类**：创建一个Java类，实现`BeanPostProcessor`接口，该接口中包含了两个方法：`postProcessBeforeInitialization()`和`postProcessAfterInitialization()`，分别用于在Bean初始化前后进行处理。
```java
import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.BeanPostProcessor;

public class CustomBeanPostProcessor implements BeanPostProcessor {
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        // 在初始化之前对Bean进行处理
        return bean;
    }

    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        // 在初始化之后对Bean进行处理
        return bean;
    }
}
```
**配置后处理器**：在XML配置文件中或者使用注解方式将该后处理器配置到Spring容器中。
```xml
<bean class="com.example.CustomBeanPostProcessor"/>
```
配置的Bean后处理器对容器中的所有Bean对象都生效
#### bean的生命周期之十步
- 定位点1：在“bean后处理器”before方法之前
**检查bean是否实现了Aware的相关接口，并设置相关依赖**
- 定位点2：在“bean后处理器”before方法之后
**检查bean是否实现initializing接口，并调用接口方法**
- 定位点3：在使用bean之后，在摧毁bean之前
**检查disposableBean接口，并调用接口方法**
- **这三个点位都是在检查是否实现了某个特定的接口**
**spring容器只对singleton的bean进行完整的生命周期管理**
**如果是prototype作用域的bean，spring只负责将该bean初始化完毕，等客户端获取到bean之后，spring就不再管理该对象的生命周期了。**
#### 自己new的对象交给spring管理
```Java
public class MyClass { public static void main(String[] args) { 
// 使用自己 new 对象 
MyObject myObject = new MyObject("Object created with new"); System.out.println(myObject); 
// 使用 DefaultListableBeanFactory 接管对象的创建和管理 
DefaultListableBeanFactory beanFactory = new DefaultListableBeanFactory(); 
beanFactory.reginsterSingleton("myObject",myObject )
//从spring容器中国获取
object my = beanFactory.getBean("myObject")
System.out.println(myObject); 
```
#### bean的循环依赖问题
- 使用singleton + setter模式循环依赖不会有问题
```xml
<!-- 定义 Bean 丈夫 --> 
<bean id="husbandBean" class="com.example.丈夫" singleton="true"> <property name="name" value="张三"/> 
<property name="wife" ref="wifeBean"/> 
</bean> 
<!-- 定义 Bean 妻子 --> 
<bean id="wifeBean" class="com.example.妻子" singleton="true"> 
<property name="name" value="李四"/> 
<property name="husband" ref="husbandBean"/> 
</bean>
```
`<property name="wife" ref="wife"/>` 这行配置的意思是在丈夫类中注入一个名为 "wife" 的属性，这个属性引用了名为 "wife" 的 Bean 对象。
- `name="wife"` 表示将要设置的属性名是 "wife"。
- `ref="wife"` 表示要引用的 Bean 对象的名称是 "wife"。Spring 容器会根据名称 "wife" 来查找对应的 Bean 对象，并将其注入到当前 Bean 中的 "wife" 属性中。
- 在这个配置中，丈夫类中的 "wife" 属性会注入一个妻子对象，而妻子对象对应的就是名称为 "wife" 的 Bean 对象。
- **当 Spring 容器创建 Bean 时，如果发现循环依赖，它会采取以下步骤来解决**：
1. **提前暴露一个尚未完全初始化的对象引用：** 当 Spring 容器创建 Bean A 时，如果发现 Bean A 依赖于 Bean B，而 Bean B 又依赖于 Bean A，那么 Spring 会提前创建一个**尚未完全初始化**的 Bean A 实例，并将其暴露给 Bean B，以满足 Bean B 的依赖需求。
2. **完成对象的初始化：** Spring 容器会继续创建 Bean B，并将其注入到 Bean A 中。然后，Spring 完成 Bean A 和 Bean B 的初始化过程。
3. Spring 的循环依赖解决机制只适用于 Singleton 作用域的 Bean，并且仅限于使用 Setter 注入方式。如果循环依赖涉及到其他作用域（如都是 prototype，会反复创建新的bean对象）或者其他注入方式（如**构造函数注入**），则可能会出现问题。
#### 反射机制
- 调用一个方法包含四要素（用不用反射机制都要具备）：
	1. 调用那个对象
	2. 调用那个对象的那个方法
	3. 调用时传递什么参数
	4. 方法执行结束后的返回结果
- 使用反射机制
	- 获取类
	- 获取方法
	- 调用方法（包含四要素）
```Java
import java.lang.reflect.Method;

public class Main {
    public static void main(String[] args) throws Exception {
        // 获取类对象
        Class<?> clazz = MyClass.class;

        // 获取方法对象（后面两个参数是在重载情况下区分用的）
        Method method = clazz.getMethod("myMethod", int.class, String.class);

        // 创建对象实例（或者使用已有的实例）
        MyClass obj = new MyClass();

        // 调用方法（对象，传递的参数，调用的方法已经确定了）
        method.invoke(obj, 123, "Hello");
    }
}

class MyClass {
    public void myMethod(int number, String text) {
        System.out.println("Number: " + number + ", Text: " + text);
    }
}

```
**只有在确实需要在运行时动态地处理类和对象，或者无法在编译时知道类的具体信息的情况下，才需要使用反射机制（spring框架原理）。**
- Spring IoC 通过**工厂模式**管理对象的创建和生命周期，通过**解析 XML 配置**文件来了解应该创建哪些对象以及这些对象之间的依赖关系，然后利用**反射机制**动态地创建和初始化对象。
#### 注解式开发
- 注解式开发（之前是写配置文件）
	- Spring IoC 最初的实现是基于 XML 配置文件的方式，通过在 XML 文件中配置 Bean 的定义和它们之间的依赖关系来管理应用程序的组件。这种 XML 配置的方式可以提供很大的灵活性，但是配置文件可能会变得冗长和复杂，维护起来相对困难。
	- Spring 引入了基于注解的开发方式，也称为注解驱动的开发。通过在 Java 类上使用特定的注解来标识组件、依赖关系以及其他配置信息，Spring IoC 容器可以自动地扫描并注册这些组件，从而实现了对 Bean 的管理。
	- **注解式开发也存在一些局限性，例如无法跨越类路径进行扫描、配置信息与代码耦合等**
- spring6倡导全注解开发
	- 负责声明bean的注解常见的四个（随便一个都可以）
		- **@Component**：`@Component` 是一个通用的注解，用于表示一个受 Spring 管理的组件。如果一个类被 `@Component` 注解标记，Spring IoC 容器就会自动将其识别为一个 Bean，并进行实例化和管理。通常用于**标识普通的 Java 类作为 Spring Bean**。
		- **@Service**：`@Service` 注解通常用于标识服务层（Service Layer）的类，表示**该类提供业务逻辑的服务**。在 Spring MVC 或者 Spring Boot 中，通常将业务逻辑的实现类标记为 `@Service`。
		- **@Repository**：`@Repository` 注解通常用于标识数据访问层（Repository Layer）的类，表示**该类是用于数据库访问的组件**。在 Spring 中，`@Repository` 注解通常与 Spring 的持久化异常转换功能结合使用，将数据库访问异常转换为 Spring 的数据访问异常。
		- **@Controller**：`@Controller` 注解通常用于标识控制器层（Controller Layer）的类，表示**该类是处理 HTTP 请求的控制器**。在 Spring MVC 中，`@Controller` 注解通常用于标识处理请求的 Controller 类。
	- 注解的使用（需要aop的依赖，引入的spring-context关联中有）
		1. 加入aop依赖 
		2. 在配置文件中配置context命名空间 
		3. 在配置中指定扫描的包 
		4. 在bean类上使用注解
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xmlns:context="http://www.springframework.org/schema/context"  
xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd  
  http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">  
    <!-- 指定扫描的包名 -->  
    <context:component-scan base-package="scan"/>  
</beans>
```
**其他方式一样，获取spring容器，获取bean对象...**  
- 如果有多个扫描包
	- 用逗号隔开
	- 添加共同的父包（牺牲一部分效率）
- **选择性实例化bean**（指定特定注解格式实例化bean）
	- 在xml的context中属性use-default-filters=false  (让所有注解失效)。在context标签中使用include-filter指定注解生效。
	- 或则在xml的context中属性use-default-filters=true  (让所有注解生效，默认也是全生效)。在context标签中使用exclude-filter指定注解失效。
- 负责注入的注解
	- **@Value**：使用@value注解给bean属性赋值。可以用在属性上并且可以不提供setter方法。也可以使用在setter和构造方法（加到形参前面）上。**只能注入简单类型**
	- **@Autowired**：当 Spring IoC 容器需要创建一个 Bean，**并且这个 Bean 的某些属性需要依赖其他 Bean 时**，可以使用 `@Autowired` 注解来自动装配这些依赖关系。（根据属性bytype自动装配，不需要指定任何属性）。**注入非简单类型**。一个接口被一个类实现。在dao类（）中去调用实现类中的方法。
		- 原来是用多态，具体实例化对象。后来使用spring的xml注入对象并实例化。再到后面使用注解注入对象。
		- **此注解根据bytype自动装配。如果只使用`@Autowired`，当接口被多个类实现。在接口类型的属性上使用注解是无法完成自动装配的。**
		- 可以出现在非简单类型属性上，setter方法上，构造方法的形参前面。
		- 当只有有参构造时，并且与属性能够对应上，注解可以省略（不推荐）
	- **@Qualifier**：`@Qualifier` 注解通常**与 `@Autowired` 注解配合使用**，用于指定需要注入的 Bean 的名称。当存在多个实现相同接口的 Bean 时，通过 `@Qualifier` 注解可以指定具体要注入的 Bean。
		- 解决上面的问题，在`@Qualifier`指定bean的名称即可。**根据byname装配需要一起使用。**
	- **@Resource**：`@Resource` 注解是 **JavaEE 提供的注解之一**，在 Spring 中**也可以用于依赖注入**。它可以指定需要注入的 Bean 的名称，也可以根据类型进行注入。在 Spring 中，`@Resource` 注解通常用于注入其他资源，如 JNDI 数据源等。
		- 更通用。只适合属性和setter。
		- 使用需要导入依赖（看你用什么spring版本）
		- 未指定name，先根据属性名。再根据类型装配。
#### 全注解式开发
- 使用注解之后，其实xml配置文件中添加的东西不多，必要浪费。
- 用一个类代替xml配置文件。
```Java
@Configuration
@ComponentScan("com.example")
public class AppConfig {
}
```
#### GoF之代理模式
- 作用：
	- **控制对对象的访问**：代理对象可以用来**控制对目标对象的访问权限**。例如，代理对象可以用来检查用户是否具有访问目标对象的权限。
	- **提供额外的功能**：代理对象可以用来**提供目标对象本身不具备的功能**。例如，代理对象可以用来为目标对象添加缓存或日志记录功能。
	- **解耦对象**：代理对象可以用来解耦目标对象之间的耦合。例如，**代理对象可以用来将目标对象的实现细节隐藏起来**。
- 代理模式中的三大角色是：
	- **抽象角色**：抽象角色定义了**代理对象和目标对象**的**共同接口**。抽象角色可以是一个接口或抽象类。
	- **代理角色**：代理角色是真实角色的代理，它**实现抽象角色的接口**。代理角色可以**对真实角色进行控制和扩展**。
	- **真实角色**：真实角色是代理所代表的真实对象。真实角色负责实现具体的业务逻辑。
- 角色之间的关系
	- 抽象角色和代理角色之间是**实现关系**。代理角色必须实现抽象角色的接口。
	- 代理角色和真实角色之间是**关联关系**（指的是真实对象为代理对象的一个属性）。代理角色持有对真实角色的引用。泛化关系（继承）的耦合度高
- 静态代理的缺点：
	- **灵活性差**：静态代理需要在编译时确定代理类的行为，无法根据需要动态地创建代理对象。
	- **代码冗余**：如果需要为多个目标对象创建代理对象，则需要编写大量的重复代码。
	- **类爆炸**：如果目标对象有很多，则会导致代理类数量爆炸。
- **动态代理**是指在**运行时创建代理类**，代理类和目标类之间**没有一对一**的关系。动态代理的实现方式有两种：
	- **JDK动态代理**：使用`java.lang.reflect.Proxy`类创建代理类（只能代理接口）。
		- Proxy.newProxyInstance()方法是Java JDK提供的一个方法，用于创建动态代理对象。该方法有以下三个参数：
		- ClassLoader loader：用于加载代理类的类加载器。
		- Class<>[] interfaces：代理类要实现的接口
		- InvocationHandler h：代理类的调用处理程序
		- **通过`Proxy.newProxyInstance()`方法创建的代理对象具有以下特点：**
		- 代理对象实现了指定的接口。代理对象的方法调用会触发调用处理程序的`invoke()`方法。
		- invoke()`方法在`java.lang.reflect.InvocationHandler`接口中
		- 它会在代理对象的方法调用时被触发。在`invoke()`方法中，可以执行一些自定义的逻辑。
		- `invoke()`方法有以下三个参数：
		- **Object proxy**：代理对象。
		- **Method method**：被调用的方法。
		- **Object[] args**：方法参数。
		- 可以使用工具类封装，看起来不那么复杂。
	- CGLIB动态代理（需要添加依赖）
		- 在CGLIB动态代理中，代理类是目标类的子类
		- **当调用代理对象的方法时，实际上会调用代理类重写的方法**。在代理类的方法中，可以执行一些自定义的逻辑
```java
// 定义目标类
class Target {
    public void sayHello() {
        System.out.println("Hello, world!");
    }
}

// 定义代理类
class Proxy extends Target {
    @Override
    public void sayHello() {
        System.out.println("方法调用之前");
        // 调用父类方法
        super.sayHello();
        System.out.println("方法调用之后");
    }
}

// 创建Enhancer对象
Enhancer enhancer = new Enhancer();

// 设置Enhancer对象的属性
enhancer.setSuperclass(Target.class);
enhancer.setCallback(new MethodInterceptor() {
    @Override
    public Object intercept(Object obj, Method method, Object[] args, MethodProxy proxy) throws Throwable {
        System.out.println("方法调用之前");
        // 调用目标方法
        Object result = proxy.invokeSuper(obj, args);
        System.out.println("方法调用之后");
        return result;
    }
});

// 创建动态代理类
Class<?> proxyClass = enhancer.create();

// 创建动态代理对象
Proxy proxy = (Proxy) proxyClass.newInstance();

// 调用代理对象的方法
proxy.sayHello();
```
#### AOP面向切面编程（底层使用动态代理实现）
- spring中的AOP的使用的动态代理：JDK动态代理和CGLIB动态代理技术
- **切面**：通常用于处理与业务逻辑无关的横切关注点，如日志记录、性能监控、事务管理等。单独提出来，只关注核心程序。需要时就切入即可，只需要写一遍。
- **AOP的七大术语如下：**
1. **连接点**：程序执行过程中的特定点，可以织入切面的位置。方法执行前后，异常抛出后等位置。
2. **切点**：真正织入切面的那个方法（一个切点对应对多个连接点）。
3. **通知**：具体的增强代码。
	- **前置通知**：在切入点之前执行的通知。
	- **后置通知**：在切入点之后执行的通知，无论切入点是否正常执行。
	- **返回通知**：在切入点正常执行之后执行的通知。
	- **异常通知**：在切入点抛出异常之后执行的通知。
	- **环绕通知**：环绕切入点的执行（前和后），可以控制切入点的执行流程。
1. **切面**：切点+通知=切面。
2. **代理对象**：AOP框架用于将切面代码织入到目标代码中的对象。
3. **织入**：将切面代码织入到目标代码中，形成最终的程序。
4. **目标对象**：被切面代码织入的对象。
- 切点表达式是 AOP 框架用来定义切入点的表达式。切点表达式可以匹配特定的连接点，从而**指定切面代码（通知）将在程序的哪些地方执行**。
	- execution(modifiers? ret-type? declaring-type? method-name(param-list?))
	- - **modifiers**：方法的修饰符(可选)，例如 `public`、`private`、`protected` 等。
	- **ret-type**：方法的返回值类型（必填），例如 `void`、`int`、`String` 等。
	- **declaring-type**：方法所在的类的类型（可选），例如 com.example.MyClass。
	- **method-name**：方法的名称（必填）。
	- **param-list**：方法的参数列表（必填），例如 `(int arg1, String arg2)`。
- spring的AOP使用（做项目没时间看）
	- 