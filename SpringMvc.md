# 关于Idea配置Spring MVC
----

## 一：基于Maven下配置Spring MVC
- 创建maven项目工程，设置配置好相关信息

 ![maven](https://i.imgur.com/85EeuJ2.png)

---
## 二：在pom.xml添加spring mvc依赖
	<!-- 阿里云maven资源库 -->
	<repositories>
		<repository>
		<id>alimaven</id>
		<name>aliyun maven</name>
		<url>http://maven.aliyun.com/nexus/content/groups/public/</url>
		</repository>
	</repositories>
	<properties>
		<!-- 项目编译的源码字符编码 -->
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<!-- 编译后的字符编码 -->
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<!--配置后相关的版本不会随着添加依赖变动-->
		<maven.compiler.source>1.8</maven.compiler.source>
		<maven.compiler.target>1.8</maven.compiler.target>
		<spring.version>5.0.1.RELEASE</spring.version>
	</properties>
	<dependencies>
	<dependency>
		<groupId>junit</groupId>
		<artifactId>junit</artifactId>
		<version>4.12</version>
		<scope>test</scope>
	</dependency>
	<!--spring 相关的依赖-->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-context</artifactId>
		<version>${spring.version}</version>
	</dependency>
	<!--配置Spring-JDBC依赖-包含tx-->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-jdbc</artifactId>
		<version>${spring.version}</version>
	</dependency>
	<!--添加spring aspects依赖-->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-aspects</artifactId>
		<version>${spring.version}</version>
	</dependency>
	<!--spring test 依赖-->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-test</artifactId>
		<version>${spring.version}</version>
	</dependency>
	<!--spring mvc-->
	<dependency>	
		<groupId>org.springframework</groupId>
		<artifactId>spring-webmvc</artifactId>
		<version>${spring.version}</version>
	</dependency>
	<!--jstl 依赖-->
	<dependency>
		<groupId>jstl</groupId>
		<artifactId>jstl</artifactId>
		<version>1.2</version>
	</dependency>
	<dependency>
		<groupId>javax</groupId>
		<artifactId>javaee-api</artifactId>
		<version>7.0</version>
	</dependency>
	</dependencies>
## 三、前端控制器配置web.xml
	<servlet>
    <!-- 核心控制器-->
    <servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <!--通過初始化參數contextConfigLocation指定springmvc配置文件的路徑-->
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:/springMvc.xml</param-value>
    </init-param>
    <!-- 当应用启动时加载该servlet -->
    <load-on-startup>1</load-on-startup>
	</servlet>
	<servlet-mapping>
     <servlet-name>dispatcherServlet</servlet-name>
     <!--
     /:支持RESTful，便于检索。
     /*:不能返回视图。
	 *.do(必须以.do结尾的路径才能访问。)
     -->
    <url-pattern>/</url-pattern>
	</servlet-mapping>
## 四、在resources配置springMvc.xml文件（可自定义）

	<!--开启自动扫描包-->
    <context:component-scan base-package="com.hore.demo.controller"/>
    <!--开始springMVC注解-->
    <mvc:annotation-driven></mvc:annotation-driven>
     <!-- HandlerMapping -->
    <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"></bean>
    <!-- HandlerAdapter -->
    <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"></bean>
    <!--配置ViewResolver-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"></property>
        <property name="prefix" value="/WEB-INF/page/"/>
        <property name="suffix" value=".jsp"/>
    </bean>





	