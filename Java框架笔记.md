## git

### 1、 删除缓存

```shell
	git rm -r -f --cached ./  
```

### 2、 初次提交的命令

```shell
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin git@github.com:xxxx.git #连接到远程的仓库
    git push -u origin master
```
### 3、 提交代码

```shell
	1. git add .
	2. git commit -m "xxx"
	3. git pull origin xxx(远程分支名) 
		这是下拉代码，将远程最新的代码先跟你本地的代码合并一下，如果确定远程没有更新，可以不用这个，执行后如果有冲突就解决，再执行1、2
	4. git push origin master
```
### 4、git五个常用命令

```shell
git clone +url
git add +文件
git commit -m +提交信息
git push
git pull
```

### 5、git 分支操作

```shell
git branch -a 创建a分支
git branch 查看分支
git checkout
git checkout -b 切换b分支
git branch -dg
```

### 6、本地上传文件到码云

首先你需要创建一个仓库，比如我的是partner，代码选择公开public，其它选项默认就好了。
在本地电脑随便创建一个文件夹，比如我的是partner,然后使用git bash，输入命令git init
在partner文件中创建一个文件，比如readme.txt：内容随便
再使用git add readme.txt、git commit -m "my git" 上传到git仓库 
再使用git remote add origin git@gitee.com:username/repositroy ,username：是你的用户名，repository是你建的仓库
再使用git pull --rebase 仓库url，保持git仓库与码云仓库一致
再使用git push gitee master 上传到远程仓库，打开码云查看仓库，就有你的文件了

### 7、创建新仓库的指令

git init //把这个目录变成Git可以管理的仓库
git add README.md //文件添加到仓库
git add . //不但可以跟单一文件，还可以跟通配符，更可以跟目录。一个点就把当前目录下所有未追踪的文件全部add了 
git commit -m "first commit" //把文件提交到仓库
git remote add origin git@github.com:yourname/youremail.git //关联远程仓库
git push -u origin master //把本地库的所有内容推送到远程库上

### 8、git连接gitee笔记

#### #首先参照

https://blog.csdn.net/zhangyu4863/article/details/80427289

#### #然后需要注意，在办公室无法使用 git remote add origin git@gitee.com:你的gitee用户名/仓库名.git

#### 可以参照如下链接教程中的切换成 https协议连接github

https://blog.csdn.net/s740556472/article/details/80318886

#### 切换成 https协议连接github

依然是先查看当前远程仓库使用的那种协议连接：

```
$ git remote -v
origin  git@github.com:unlimitbladeworks/Data-Struts-Learning.git (fetch)
origin  git@github.com:unlimitbladeworks/Data-Struts-Learning.git (push)
```

移除掉远程仓库的配置

```
$ git remote rm origin
```

重新添加新的远程仓库，以https的形式：

```
git remote add origin https://github.com/unlimitbladeworks/Data-Struts-Learning.git
```

再次查看:

```
$ git remote -v
origin  https://github.com/unlimitbladeworks/Data-Struts-Learning.git (fetch)
origin  https://github.com/unlimitbladeworks/Data-Struts-Learning.git (push)
```

 

#### #最后遇到的问题是git push没有报错， 但是远程仓库没有更新的问题，可以使用如下指令：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 $ git checkout master  

 $ git merge rowsizectrl(这里换成你的分支名字)

 $ git branch -d rowsizectrl ##当前分支已经没用了，记得删除，如果你还要用就不要删除了

 $ git push -u origin master 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

参考链接为https://blog.csdn.net/yban10032/article/details/81903675

####  #补充下，换台电脑拉取远程库的操作

$git pull

参考链接

https://blog.csdn.net/QH_JAVA/article/details/77760499

 

#### #补充， git基本操作语法

https://www.cnblogs.com/gavincoder/p/9073368.html

#### #补充，git commit弹出Please enter a commit message to explain why this merge is necessary.

https://www.cnblogs.com/quan-coder/p/8478015.html

 

#### #补充,git远程分支与本地分支合并

https://blog.csdn.net/xiasohuai/article/details/81980112

 

\#补充Git - git config 查看配置信息

查看系统config

```
git config --system --list
```

查看当前用户（global）配置

```
git config --global  --list
```

查看当前仓库配置信息

```
git config --local  --list
```

## IDEA

在启动tomcat之后，出现404资源未找到错误，查看打包发布的out目录，其中没有web目录下的jsp文件，自然无法找到。

解决方法：在Project Structure Artifacts里面 添加JavaEE facet Resource把web包加进去。一般在移动了项目目录会出现。

### debug

step over 走一步 但是不进入方法

step into 进入方法，但是不进入jdk源代码

Force step into 强制进入方法，进入的比较狠，会进入源代码

step out 出方法

Run to Cursor 运行到光标处

## maven

### 	1、在conf/setting.xml中更改JDK版本

```xml
	<profile>    

	    <id>jdk-1.8</id>    
	
	     <activation>    
	
	        <activeByDefault>true</activeByDefault>    
	
	        <jdk>1.8</jdk>    
	
	      </activation>    
	
	    <properties>    
	
	        <maven.compiler.source>1.8</maven.compiler.source>    
	
	        <maven.compiler.target>1.8</maven.compiler.target>
	
	        <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion> 
	
	    </properties>    
	
	</profile>
```
### 2、在pom.xml中指定JDK版本

```xml
<build>  

    <plugins>  

        <plugin>  

            <groupId>org.apache.maven.plugins</groupId>

            <artifactId>maven-compiler-plugin</artifactId>  

                <version>3.7</version>  

                <configuration>  

                    <source>1.8</source>  

                    <target>1.8</target>  

                </configuration>  

            </plugin>  

        </plugins>  

</build>
```

###  3、**Maven静态资源过滤问题** 

可能会扫描不到xml文件，可在class文件夹中查看，如果没有，在pom文档中加入如下代码

```xml
<build>
    <resources>
       <resource>
           <directory>src/main/java</directory>
           <includes>
               <include>**/*.properties</include>
               <include>**/*.xml</include>
           </includes>
           <filtering>false</filtering>
       </resource>
       <resource>
           <directory>src/main/resources</directory>
           <includes>
               <include>**/*.properties</include>
               <include>**/*.xml</include>
           </includes>
           <filtering>false</filtering>
       </resource>
    </resources>
</build>
```

## Mybatis

### 1、mybatis核心配置文件

  一般命名为 mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
       PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
       "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
   <environments default="development">
       <environment id="development">
           <transactionManager type="JDBC"/>
           <dataSource type="POOLED">
               <property name="driver" value="com.mysql.jdbc.Driver"/>
               <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=utf8"/>
               <property name="username" value="root"/>
               <property name="password" value="123456"/>
           </dataSource>
       </environment>
   </environments>
   <mappers>
       <mapper resource="com/kuang/dao/userMapper.xml"/>
   </mappers>
</configuration>
```

在核心配置文件中加入其他配置，如配置文件、日志、给实体类起别名

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>
    <!--    properties引入外部配置文件-->
    <properties resource="db.properties"></properties>
    <settings>
<!--        标准的日志工厂实现-->
<!--        <setting name="logImpl" value="STDOUT_LOGGING"/>-->
        <setting name="logImpl" value="LOG4J"/>
    </settings>
    <!--    typeAliases可以给实体类起别名-->
<!--    方式一,给指定类起别名-->
<!--    <typeAliases>-->
<!--        <typeAlias type="com.yyy.pojo.User" alias="User"/>-->
<!--    </typeAliases>-->
<!--    方式二,扫描实体类的包，自动起别名，当实体类较多建议用方式二-->
<!--    方式一可以自定义别名，方式二不行，但是如果类中包含@Alias("xxxx")注解，则别名为注解值-->
    <typeAliases>
        <package name="com.yyy.pojo"/>
    </typeAliases>

    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>

    <mappers>
<!--        一：使用resource(绑定配置文件),配置文件可在任意位置-->
<!--        <mapper resource="com/yyy/dao/UserMapper.xml"/>-->
<!--        二：使用class(绑定接口) 可使用注解-->
        <mapper class="com.yyy.dao.UserMapper"></mapper>
    </mappers>

</configuration>
```



### 2、mapper.xml

有可能在文件中加中文注释报错，将头文件中UTF-8改为UTF8错误消失

```xml
<?xml version="1.0" encoding="UTF8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--加注释会报错 将utf-8改为utf8错误消失-->
<!--namespace是接口类的全名-->
<!--id是接口中的方法名 resultType是方法的返回值类型-->
<mapper namespace="com.yyy.dao.UserMapper">
    <select id="getUserList" resultType="com.yyy.pojo.User">
        select * from user
    </select>
    <select id="getUserByID" parameterType="int" resultType="com.yyy.pojo.User">
        select * from user where id = #{id}
    </select>

    <select id="getUserLike" resultType="com.yyy.pojo.User">
        select * from user where name like ${value};
    </select>

    <insert id="InsertUser" parameterType="com.yyy.pojo.User">
        insert into user (id,name,pwd) values (#{id},#{name},#{pwd});
    </insert>
    <update id="UpdateUser" parameterType="com.yyy.pojo.User">
        update user set name = #{name} ,pwd = #{pwd} where id = #{id};
    </update>
    <delete id="DeleteUser" parameterType="int">
        delete from user where id = #{id};
    </delete>
</mapper>
```

### 3、Mybatis常用工具类

MybatisUtils.java  getSqlSessoion()方法来获取sqlSession  其中包含是否开启事务自动提交的参数

获取sqlSession使用以后，要调用sqlSession.close()来关闭连接

```java
package com.yyy.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

public class MybatisUtils {
    private static SqlSessionFactory sqlSessionFactory;
    static {
        try {
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    public static SqlSession getSqlSessoion(){
        return sqlSessionFactory.openSession(true);//参数表示是否开启事务自动提交
    }
}
```

数据库配置文件db.properties

```properties
driver = com.mysql.cj.jdbc.Driver
url = jdbc:mysql://localhost:3306/mybatis?useSSL=true&useUnicode=true&characterEncoding=utf8&serverTimezone=UTC
username = root
password = root
```



## SpringMVC

dao层+service层：mvc的modle层

### 1、可能出现的错误

IDEA启动WEB项目，出现404，查看jar包，有可能是本地项目有jar包，但tomcat发布的项目中，没有添加jar包

```
1、打开Project Structure
2、Artifacts
3、Output Layout
4、在WEB-INF下添加lib
5、点加号把项目jar包添加进来
```

### 2、Spring的配置文件

官方名称一般为 [servletname]-servlet.xml 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

</beans>
```

处理映射器：就是找到controller

```xml
<bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
```

处理器适配器：就是去执行controller

```xml
<bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>
```

视图解析器：就是选择显示哪个视图，把名字拼接起来显示给用户

```xml
<!--视图解析器:DispatcherServlet给他的ModelAndView-->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="InternalResourceViewResolver">
   <!--前缀-->
   <property name="prefix" value="/WEB-INF/jsp/"/>
   <!--后缀-->
   <property name="suffix" value=".jsp"/>
</bean>
```

（实际开发不用这个，使用注解版）

### 3、杂记

@RequestParam("xxx") 参数前有这个注解，表示该参数一定是从前端接收参数，所以不论变量名是否一样，都建议加上该注解



## Spring

### 1、动态代理机制中invoke()方法

Proxy.newProxyInstance(ClassLoader loader,Class[] interfaces,InvocationHandler h)参数分别为 

- 被代理的类（真实角色，就是实现了接口方法的实现类）
- 被代理接口的所有方法
- 实现了InvocationHandler接口的类

个人理解：

1. 实现InvocationHandler接口的类必定重写invoke(...)方法，该方法不显式调用，而是Proxy.newProxyInstance(...)得到代理类实例，根据传递的方法和方法参数，实现了要代理的接口（和里面的方法）并继承了Proxy类，在执行被代理方法时，执行了super.h.invoke(...)方法，即InvocationHandler.invoke()。参考博客：https://blog.csdn.net/zcc_0015/article/details/22695647
2. 整个模式类似于黄文毅所写SpringMVC+Mybatis一书中所提到的工厂方法模式，Proxy作为总工厂，不直接代理，而是接收参数，生产各种代理，来实现特定的代理，参数中就包含InvocationHandler的实现类，实现类中有invoke方法。



### 2、@RestController @ResponseBody 

@RestController 大约= @ResponseBody +@Controller,@ResponseBody 用来阻止视图解析器解析返回的字符串，因为前后端分离的话，不需要视图解析器来解析，只需要给前端一个接口

## 3、@Bean用在方法上

告诉Spring 可以从这个方法上得到一个类

## SpringBoot

### 1、Thymeleaf pom依赖

```xml
<dependency>
<groupId>org.thymeleaf</groupId>
<artifactId>thymeleaf-spring5</artifactId>
</dependency>
<dependency>
    <groupId>org.thymeleaf.extras</groupId>
    <artifactId>thymeleaf-extras-java8time</artifactId>
</dependency>
```

### 2、SpringBoot的starter的pom依赖

官网：https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-starter

### 3、springsecurity与thymeleaf的整合命名空间

```html
<html lang="en" xmlns:th="http://www.thymeleaf.org" 
      xmlns:sec="http://www.thymeleaf.org/thymeleaf-extras-springsecurity5">
```

### 4、WebMvcConfigurer

## 1. 简介

WebMvcConfigurer配置类其实是`Spring`内部的一种配置方式，采用`JavaBean`的形式来代替传统的`xml`配置文件形式进行针对框架个性化定制，可以自定义一些Handler，Interceptor，ViewResolver，MessageConverter。基于java-based方式的spring mvc配置，需要创建一个**配置**类并实现**`WebMvcConfigurer`** 接口；

在Spring Boot 1.5版本都是靠重写**WebMvcConfigurerAdapter**的方法来添加自定义拦截器，消息转换器等。SpringBoot 2.0 后，该类被标记为@Deprecated（弃用）。官方推荐直接实现WebMvcConfigurer或者直接继承WebMvcConfigurationSupport，方式一实现WebMvcConfigurer接口（推荐），方式二继承WebMvcConfigurationSupport类，具体实现可看这篇文章。https://blog.csdn.net/fmwind/article/details/82832758

## **2. WebMvcConfigurer接口**

```java
public interface WebMvcConfigurer {
    void configurePathMatch(PathMatchConfigurer var1);
    void configureContentNegotiation(ContentNegotiationConfigurer var1);
    void configureAsyncSupport(AsyncSupportConfigurer var1);
    void configureDefaultServletHandling(DefaultServletHandlerConfigurer var1);
    void addFormatters(FormatterRegistry var1);
    void addInterceptors(InterceptorRegistry var1);
    void addResourceHandlers(ResourceHandlerRegistry var1);
    void addCorsMappings(CorsRegistry var1);
    void addViewControllers(ViewControllerRegistry var1);
    void configureViewResolvers(ViewResolverRegistry var1);
    void addArgumentResolvers(List<HandlerMethodArgumentResolver> var1);
    void addReturnValueHandlers(List<HandlerMethodReturnValueHandler> var1);
    void configureMessageConverters(List<HttpMessageConverter<?>> var1);
    void extendMessageConverters(List<HttpMessageConverter<?>> var1);
    void configureHandlerExceptionResolvers(List<HandlerExceptionResolver> var1);
    void extendHandlerExceptionResolvers(List<HandlerExceptionResolver> var1);
    Validator getValidator();
    MessageCodesResolver getMessageCodesResolver();
}
```

**常用的方法：**

```java
 /* 拦截器配置 */
void addInterceptors(InterceptorRegistry var1);
/* 视图跳转控制器 */
void addViewControllers(ViewControllerRegistry registry);
/**
     *静态资源处理
**/
void addResourceHandlers(ResourceHandlerRegistry registry);
/* 默认静态资源处理器 */
void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer);
/**
     * 这里配置视图解析器
 **/
void configureViewResolvers(ViewResolverRegistry registry);
/* 配置内容裁决的一些选项*/
void configureContentNegotiation(ContentNegotiationConfigurer configurer);
/** 解决跨域问题 **/
public void addCorsMappings(CorsRegistry registry) ;
```

### 2.1 addInterceptors：拦截器

- addInterceptor：需要一个实现HandlerInterceptor接口的拦截器实例
- addPathPatterns：用于设置拦截器的过滤路径规则；`addPathPatterns("/**")`对所有请求都拦截
- excludePathPatterns：用于设置不需要拦截的过滤规则
- 拦截器主要用途：进行用户登录状态的拦截，日志的拦截等。

```java
@Override
public void addInterceptors(InterceptorRegistry registry) {
    super.addInterceptors(registry);
    registry.addInterceptor(new TestInterceptor()).addPathPatterns("/**").excludePathPatterns("/emp/toLogin","/emp/login","/js/**","/css/**","/images/**");
}
```

### 2.2 addViewControllers：页面跳转

以前写SpringMVC的时候，如果需要访问一个页面，必须要写Controller类，然后再写一个方法跳转到页面，感觉好麻烦，其实重写WebMvcConfigurer中的addViewControllers方法即可达到效果了

```java
    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        registry.addViewController("/toLogin").setViewName("login");
    }
```

值的指出的是，在这里重写addViewControllers方法，并不会覆盖**WebMvcAutoConfiguration**（Springboot自动配置）中的addViewControllers（在此方法中，Spring Boot将“/”映射至index.html），这也就意味着自己的配置和Spring Boot的自动配置同时有效，这也是我们推荐添加自己的MVC配置的方式。

 

### 2.3 addResourceHandlers：静态资源

比如，我们想自定义静态资源映射目录的话，只需重写addResourceHandlers方法即可。

注：如果继承WebMvcConfigurationSupport类实现配置时必须要重写该方法，具体见其它文章

```java
@Configuration
public class MyWebMvcConfigurerAdapter implements WebMvcConfigurer {
    /**
     * 配置静态访问资源
     * @param registry
     */
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/my/**").addResourceLocations("classpath:/my/");
    }
}
```

- addResoureHandler：指的是对外暴露的访问路径
- addResourceLocations：指的是内部文件放置的目录

### 2.4 configureDefaultServletHandling：默认静态资源处理器

```java
@Override
public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
        configurer.enable();
        configurer.enable("defaultServletName");
}
```

此时会注册一个默认的Handler：DefaultServletHttpRequestHandler，这个Handler也是用来处理静态文件的，它会尝试映射/。当DispatcherServelt映射/时（/ 和/ 是有区别的），并且没有找到合适的Handler来处理请求时，就会交给DefaultServletHttpRequestHandler 来处理。注意：这里的静态资源是放置在web根目录下，而非WEB-INF 下。
　　可能这里的描述有点不好懂（我自己也这么觉得），所以简单举个例子，例如：在webroot目录下有一个图片：1.png 我们知道Servelt规范中web根目录（webroot）下的文件可以直接访问的，但是由于DispatcherServlet配置了映射路径是：/ ，它几乎把所有的请求都拦截了，从而导致1.png 访问不到，这时注册一个DefaultServletHttpRequestHandler 就可以解决这个问题。其实可以理解为DispatcherServlet破坏了Servlet的一个特性（根目录下的文件可以直接访问），DefaultServletHttpRequestHandler是帮助回归这个特性的。

 

### 2.5 configureViewResolvers：视图解析器

这个方法是用来配置视图解析器的，该方法的参数ViewResolverRegistry 是一个注册器，用来注册你想自定义的视图解析器等。ViewResolverRegistry 常用的几个方法：https://blog.csdn.net/fmwind/article/details/81235401

```java
/**
 * 配置请求视图映射
 * @return
 */
@Bean
public InternalResourceViewResolver resourceViewResolver()
{
	InternalResourceViewResolver internalResourceViewResolver = new InternalResourceViewResolver();
	//请求视图文件的前缀地址
	internalResourceViewResolver.setPrefix("/WEB-INF/jsp/");
	//请求视图文件的后缀
	internalResourceViewResolver.setSuffix(".jsp");
	return internalResourceViewResolver;
}
/**
 * 视图配置
 * @param registry
 */
@Override
public void configureViewResolvers(ViewResolverRegistry registry) {
	super.configureViewResolvers(registry);
	registry.viewResolver(resourceViewResolver());
	/*registry.jsp("/WEB-INF/jsp/",".jsp");*/
}
```

### 2.6 configureContentNegotiation：配置内容裁决的一些参数

### 2.7 addCorsMappings：跨域

```java
@Override
public void addCorsMappings(CorsRegistry registry) {
    super.addCorsMappings(registry);
    registry.addMapping("/cors/**")
            .allowedHeaders("*")
            .allowedMethods("POST","GET")
            .allowedOrigins("*");
}
```

### 2.8 configureMessageConverters：信息转换器

```java
/**
* 消息内容转换配置
 * 配置fastJson返回json转换
 * @param converters
 */
@Override
public void configureMessageConverters(List<HttpMessageConverter<?>> converters) {
    //调用父类的配置
    super.configureMessageConverters(converters);
    //创建fastJson消息转换器
    FastJsonHttpMessageConverter fastConverter = new FastJsonHttpMessageConverter();
    //创建配置类
    FastJsonConfig fastJsonConfig = new FastJsonConfig();
    //修改配置返回内容的过滤
    fastJsonConfig.setSerializerFeatures(
            SerializerFeature.DisableCircularReferenceDetect,
            SerializerFeature.WriteMapNullValue,
            SerializerFeature.WriteNullStringAsEmpty
    );
    fastConverter.setFastJsonConfig(fastJsonConfig);
    //将fastjson添加到视图消息转换器列表内
    converters.add(fastConverter);
}
```

