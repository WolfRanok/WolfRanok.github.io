---
layout: post
title: Java EE
author: Ranok
tags: [java,java ee, 期末考试]     #标签会影响
feature-img: "assets/img/feature-img/javaee.jpg" # 这是一个会出现在博客文章内部的图片
thumbnail: "assets/img/thumbnails/feature-img/javaee.jpg" # 这是一个会出现在博客外部的图片
permalink: javaee # 这条会将该界面的URL自定义
---

&emsp;&emsp;Java EE，Java 平台企业版（Java Platform Enterprise Edition），之前称为Java 2 Platform, Enterprise Edition (J2EE)，2018年3月更名为 Jakarta EE(这个名称应该还没有得到群众认可)。是 Sun 公司为企业级应用推出的标准平台，用来开发B/S架构软件。Java EE 可以说是一个框架，也可以说是一种规范。

---

## 前言
&emsp;&emsp;《java EE》是一门与就业相关度较高的一门课程，作为企业级的应用开发，虽然书本上学的ssm框架已经过时，但是作为我们初学者，它的价值还是不小的。

&emsp;&emsp;本博客按知识点整理一些相关内容，祝愿你可以取得一个让自己满意的成绩。

---
## 问题解析
#### Spring中Bean的作用域有哪些，默认是哪一个

&emsp;&emsp;singleton：单例模式（**默认**），在整个Spring IoC容器中，使用singleton定义的Bean将只有一个实例

&emsp;&emsp;prototype：原型模式，每次通过容器的getBean方法获取prototype定义的Bean时，都将产生一个新的Bean实例

&emsp;&emsp;request：对于每次HTTP请求，使用request定义的Bean都将产生一个新实例，即每次HTTP请求将会产生不同的Bean实例。只有在Web应用中使用Spring时，该作用域才有效

&emsp;&emsp;session：对于每次HTTP Session，使用session定义的Bean豆浆产生一个新实例。同样只有在Web应用中使用Spring时，该作用域才有效

&emsp;&emsp;globalsession：每个全局的HTTP Session，使用session定义的Bean都将产生一个新实例。典型情况下，仅在使用portlet context的时候有效。同样只有在Web应用中使用Spring时，该作用域才有效

---

#### Spring中有哪些注解
&emsp;&emsp;1. @Controller：将Controller层的类对象交由spring容器生成与管理

&emsp;&emsp;2. @Service：将Service层的类对象交由spring容器生成与管理

&emsp;&emsp;3. @Repository：将Dao层的类对象交由spring容器生成与管理

&emsp;&emsp;4. @Component将类对象交由spring容器生成与管理

---

#### Spring AOP、IOC的概念
&emsp;&emsp;AOP(Aspect-Oriented Programming:面向切面编程)：是指将那些与业务无关，却被多个业务模块所共同调用逻辑或责任（例如事务处理、日志管理、权限控制等）封装起来，便于减少系统的重复代码，降低模块间的耦合度，提升系统的可维护性。

&emsp;&emsp;IOC就是控制反转，是指程序将创建对象的控制权转交给Spring框架进行管理，由Spring通过java的反射机制根据配置文件在运行时动态的创建实例，并管理各个实例之间的依赖关系。

---

#### Spring AOP中的通知类型

| 通知类型 | 注解 | 说明 |
|:-:|:-:|:-:|
|before（前置通知） | @Before | 通知方法在目标方法调用之前执行|
|after（后置通知）|@After|通知方法在目标方法返回或异常后调用|
|after-returning（返回通知）|	@AfterReturning	|通知方法会在目标方法返回后调用|
|after-throwing（异常抛出通知）	|@AfterThrowing	|通知方法会在目标方法抛出异常后调用|
|around（环绕通知）|	@Around|	通知方法会将目标方法封装起来|

---

#### Spring 实现AOP的动态代理的方式

&emsp;&emsp;1. JDK动态代理（基于接口实现的）：JDK动态代理制能对实现了接口的类生成代理，而不是针对类

&emsp;&emsp;2. CGLIB动态代理（基于类实现的）：CGLIB是针对类实现代理，主要对指定的类生成一个子类，覆盖其中的方法，添加额外功能，因为是继承，所以该类方法不能用final来声明。

---

#### MyBaes如何防止SQL注入问题

&emsp;&emsp;在编写MyBatis的映射语句时，尽量采用“#{xxx}”这样的格式。若不得不使用“${xxx}”这样的参数，要手工地做好过滤工作，来防止SQL注入攻击。

---

#### 动态SQL的使用

```xml
<select id="queryList" parameterType="com.jinzheng.pojo.Book" resultType="com.jinzheng.pojo.Book">
    select * from tb_book
    <where>
        <if test="id != null and id !='' ">
            or id = #{id}
        </if>
        <if test="name != null and name !='' ">
            or name like concat('%',#{name},'%')
        </if>
        <if test="press != null and press !='' ">
            or press like concat('%',#{press},'%')
        </if>
        <if test="author != null and author !='' ">
            or author like concat('%',#{author},'%')
        </if>
        <if test="bookPrice != null and bookPrice !='' ">
            or bookPrice = #{bookPrice}
        </if>
    </where>
</select>
```

---

#### Spring MVC的工作原理
{% include aligner.html images="blog-img/javaee/1.png" %}

---

#### 开发Java Web项目的三层架构

&emsp;&emsp;1)：数据访问层：(dao持久层)主要是对原始数据（数据库或者文本文件等存放数据的形式）的操作层，
而不是指原始数据，也就是说，是对数据的操作，而不是数据库，具体为业务逻辑层或表示层
提供数据服务．

&emsp;&emsp;2)：业务逻辑层：(service)主要是针对具体的问题的操作，也可以理解成对数据层的操作，对数据业务
逻辑处理，如果说数据层是积木，那逻辑层就是对这些积木的搭建。具体的讲主要负责对数
据层的操作。也就是说把一些数据层的操作进行组合。

&emsp;&emsp;3)：表示层：(controller)主要表示WEB方式，如果逻辑层相当强大和完善，
无论表现层如何定义和更改，逻辑层都能完善地提供服务。
主要对用户的请求接受，以及数据的返回，为客户端提供应用程序的访问。

---

#### serverlet需要实现的两个方法是什么
&emsp;&emsp;1. toGet 方法<br>
&emsp;&emsp;2. toPut 方法<br>

####  JSP的9个内置对象

&emsp;&emsp;1. Request对象<br>
&emsp;&emsp;2. Response对象<br>
&emsp;&emsp;3. Out对象<br>
&emsp;&emsp;4. session对象<br>
&emsp;&emsp;5. Application对象<br>
&emsp;&emsp;6. PageContext对象<br>
&emsp;&emsp;7. Config对象<br>
&emsp;&emsp;8. Page（相当于this）对象<br>
&emsp;&emsp;9. Exception对象

---

#### 程序设计题
##### 1. MyBean
设计一个数据库访问的代码：

```java
public void userFindByIdTest() {
    String resources = "mybatis-config.xml";
    Reader reader = null;
    try {
        reader = Resources.getResourceAsReader(resources);
    } catch (IOException e) {
        e.printStackTrace();
    }
    SqlSessionFactory sqlMapper = new SqlSessionFactoryBuilder().build(reader);
    SqlSession session = sqlMapper.openSession();
    User user = session.selectOne("findById", 1);
    System.out.println(user.getUname());
    session.close();
}
```

##### 2. AOP
基于注解的AOP代码：

###### 注册bean

```xml
<bean name="userDao" class="com.itheima.demo03.UserDaoImpl"/>
<bean name="AnnoAdvice" class="com.itheima.demo04.AnnoAdvice"/>
<!-- 开启@aspectj的自动代理支持 -->
<aop:aspectj-autoproxy/>

```

###### 定义通知
```java
/**
 * 1、在切面中，需要通过指定的注解将方法标识为通知方法
 * @Before：前置通知，在目标对象方法执行之前执行
 * @After：后置通知，在目标对象方法的finally字句中执行
 * @AfterReturning：返回通知，在目标对象方法返回值之后执行
 * @AfterThrowing：异常通知，在目标对象方法的catch字句中执行
 *
 * 2、切入点表达式：设置在标识通知的注解的value属性中
 * execution(public int com.atguigu.spring.aop.annotation.CalculatorImpl.add(int, int)
 * execution(* com.atguigu.spring.aop.annotation.CalculatorImpl.*(..)
 * 第一个*表示任意的访问修饰符和返回值类型
 * 第二个*表示类中任意的方法
 * ..表示任意的参数列表
 * 类的地方也可以使用*，表示包下所有的类
 * 3、重用切入点表达式
 * //@Pointcut声明一个公共的切入点表达式
 * @Pointcut("execution(* com.atguigu.spring.aop.annotation.CalculatorImpl.*(..))")
 * public void pointCut(){}
 * 使用方式：@Before("pointCut()")
 *
 * 4、获取连接点的信息
 * 在通知方法的参数位置，设置JoinPoint类型的参数，就可以获取连接点所对应方法的信息
 * //获取连接点所对应方法的签名信息
 * Signature signature = joinPoint.getSignature();
 * //获取连接点所对应方法的参数
 * Object[] args = joinPoint.getArgs();
 *
 */
 
@Component
@Aspect  //将当前组件标识为切面
public class LoggerAspect {
 
    @Pointcut("execution(* com.atguigu.spring.aop.annotation.CalculatorImpl.*(..))")
    public void pointCut(){}
 
    //前置通知
    //@Before("execution(public int com.atguigu.spring.aop.annotation.CalculatorImpl.add(int, int))")
    //@Before("execution(* com.atguigu.spring.aop.annotation.CalculatorImpl.*(..))")
    @Before("pointCut()")
    public void beforeAdviceMethod(JoinPoint joinPoint) {
        //获取连接点所对应方法的签名信息
        Signature signature = joinPoint.getSignature();
        //获取连接点所对应方法的参数
        Object[] args = joinPoint.getArgs();
        System.out.println("LoggerAspect，方法："+signature.getName()+"，参数："+ Arrays.toString(args));
    }
 
    //后置通知
    @After("pointCut()")
    public void afterAdviceMethod(JoinPoint joinPoint){
        // System.out.println("LoggerAspect,后置通知");
        //获取连接点所对应方法的签名信息
        Signature signature = joinPoint.getSignature();
        System.out.println("LoggerAspect，方法："+signature.getName()+"，执行完毕");
    }
 
    //返回通知
    /**
     * 在返回通知中若要获取目标对象方法的返回值
     * 只需要通过@AfterReturning注解的returning属性
     * 就可以将通知方法的某个参数指定为接收目标对象方法的返回值的参数
     */
    @AfterReturning(value = "pointCut()", returning = "result")
    public void afterReturningAdviceMethod(JoinPoint joinPoint, Object result){
        // System.out.println("LoggerAspect,返回通知");
        //获取连接点所对应方法的签名信息
        Signature signature = joinPoint.getSignature();
        System.out.println("LoggerAspect，方法："+signature.getName()+"，结果："+result);
    }
 
      //异常通知
    @AfterThrowing( "pointCut()")
    public void afterThrowingAdviceMethod(JoinPoint joinPoint){
        //获取连接点所对应方法的签名信息
        Signature signature = joinPoint.getSignature();
        System.out.println("LoggerAspect，方法："+signature.getName()+",异常通知");
    }
 
    /**
     * 在异常通知中若要获取目标对象方法的异常
     * 只需要通过AfterThrowing注解的throwing属性
     * 就可以将通知方法的某个参数指定为接收目标对象方法出现的异常的参数
     */
    @AfterThrowing(value = "pointCut()", throwing = "ex")
    public void afterThrowingAdviceMethod(JoinPoint joinPoint, Throwable ex){
        //获取连接点所对应方法的签名信息
        Signature signature = joinPoint.getSignature();
        System.out.println("LoggerAspect，方法："+signature.getName()+"，异常："+ex);
    }
 
 
    //环绕通知
    @Around("pointCut()")
    //环绕通知的方法的返回值一定要和目标对象方法的返回值一致
    public Object aroundAdviceMethod(ProceedingJoinPoint joinPoint){
        Object result = null;
        try {
            System.out.println("环绕通知-->前置通知");
            //表示目标对象方法的执行
            result = joinPoint.proceed();
            System.out.println("环绕通知-->返回通知");
        } catch (Throwable throwable) {
            throwable.printStackTrace();
            System.out.println("环绕通知-->异常通知");
        } finally {
            System.out.println("环绕通知-->后置通知");
        }
        return result;
    }
}
```

#### MyBean XML程序编写
要求写出对应的增删改查的几种代码

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.jinzheng.dao.BookMapper">

<!--    显示所有目录-->
    <select id="findAll" resultType="com.jinzheng.pojo.Book">
        select * from tb_book
    </select>

<!--    根据id查询图书信息 -->
    <select id="findBookById" parameterType="Integer"
            resultType="com.jinzheng.pojo.Book">
        select *
        from tb_book
        where id=#{id}
    </select>

<!--    添加数据-->
    <insert id="addBook" parameterType="com.jinzheng.pojo.Book">
        insert into tb_book values (#{id},#{name},#{press},#{author},#{bookPrice})
    </insert>

<!--        删除数据-->
    <delete id="deleteById" parameterType="Integer">
        delete from tb_book where id = #{id}
    </delete>

<!--    修改数据-->
    <update id="updateBook" parameterType="com.jinzheng.pojo.Book">
        update tb_book
        <set>
            <if test="name != null and name != '' ">
                name = #{name},
            </if>
            <if test="press != null and press != '' ">
                press = #{press},
            </if>
            <if test="author != null and author != '' ">
                author = #{author},
            </if>
            <if test="bookPrice != null and bookPrice != '' ">
                bookPrice = #{bookPrice},
            </if>

        </set>
        where id = #{id}
    </update>

<!--        根据图书信息去模糊查询图书信息(动态SQL)-->
    <select id="queryList" parameterType="com.jinzheng.pojo.Book" resultType="com.jinzheng.pojo.Book">
        select * from tb_book
        <where>
            <if test="id != null and id !='' ">
                or id = #{id}
            </if>
            <if test="name != null and name !='' ">
                or name like concat('%',#{name},'%')
            </if>
            <if test="press != null and press !='' ">
                or press like concat('%',#{press},'%')
            </if>
            <if test="author != null and author !='' ">
                or author like concat('%',#{author},'%')
            </if>
            <if test="bookPrice != null and bookPrice !='' ">
                or bookPrice = #{bookPrice}
            </if>
        </where>
    </select>

</mapper>

```