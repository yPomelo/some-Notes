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
    git remote add origin git@github.com:xxxx.git
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



## IDEA

在启动tomcat之后，出现404资源未找到错误，查看打包发布的out目录，其中没有web目录下的jsp文件，自然无法找到。

解决方法：在Project Structure Artifacts里面 添加JavaEE facet Resource把web包加进去。一般在移动了项目目录会出现。

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