---
layout: post
title: "Spring WEB MVC总结"
date: 2013-05-27 00:26
comments: true
categories: [spring,java,web,mvc]
---

用了这么久的spring web，终于把官方的文档看了看，总结出来下面的文档。

<!-- more -->

####Spring WEB MVC的特性

* 角色分明：controller、validator、command object、form object、model object、DispatcherServlet、handler mapping、view resolver等等，每个角色都可以由一个专门的对象来实现；
* 框架和类似JavaBean应用类的强大而简单的配置；
* 适配性、非侵入性以及灵活性。可以任意定义controller方法的前面，对于指定的场景，可以使用@RequestParam、@RequestHeader、@PathVariable其中的一个；
* 可重用的业务代码；
* 可定制话的绑定和验证；
* 类型匹配错误作为应用层的验证错误，取代手动将传进来的String-Only对象parse and convert成为业务对象；
* 个性化handler mapping以及view resolution；
* 灵活的model解析。利用name/value Map，可以利用任意一种view技术解析model；
* 个性化的locale以及theme resolution。支持JSPs，包不包含Spring tag lib，JSTL都行；
* 等等

####其他MVC实现的可插入性

如果不想使用Spring web MVC，而是想在其他类似struts、WebWork的框架中使用Spring的某些特性，这也是可以的，具体的可以查看相关文档。

####DispatcherServlet类

和其他的MVC框架一样，Spring web MVC也是基于__请求驱动__的模型，围绕一个核心的servlet，将所有的请求分发到Controllers，同时提供丰富的功能，来帮助web应用程序的开发。Spring完全集成Spring IoC容器，允许你使用Spring所拥有的任何特性。

下图是Spring web MVC中的请求处理流程图：

{% img https://dl.dropboxusercontent.com/u/99113526/blog.bd17kaka.net/spring-web-mvc.png %}

DispatcherServlet是Servlet类的一个子类，继承自HttpServlet，它在web.xml文件中进行定义。需要通过使用URL映射，来将需要其处理的请求映射到这个Servlet。下面是一个标准的servlet配置：

```
<!-- web.xml -->
<web-app>

    <servlet>
        <servlet-name>example</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>example</servlet-name>
        <url-pattern>*.form</url-pattern>
    </servlet-mapping>

</web-app>
```

在这个例子中，所有满足表达式“*.form”的请求，都将有servlet-name为“example”的这个servlet来进行处理。

在Spring中，ApplicationContext实例是有作用域的。在Web MVC架构中，每一个DispatcherServlet类都有它自己的WebApplicationContext，这个WebApplicationContext继承所有已经在根部的WebApplicationContext中所定义的beans。这些beans是可以被在servlet中定义的beans所覆盖的。（不太懂，得看看Spring Ioc）

在DispatcherServlet初始化的时候，Spring在文件夹WEB-INF中查找文件名为[servlet-name]-servlet.xml的文件，并且创建那个文件里面定义的所有beans。将在全局作用域中，有相同名称的bean全覆盖掉。

考虑上面的那个web.xml定义，那么需要在WEB-INF文件夹中，创建一个名为example-servlet.xml的文件，这个里面包含所有Spring WEB MVC所拥有的beans。

__我的理解是：一个web.xml文件中可以定义多个servlet；一个servlet对应一个example-servlet.xml文件；一个example-servlet.xml文件就是一个WebApplicationContext。__

在WebApplicationContext中，包含下面这些类型的beans：

* controllers
* handler mappings
* view resolvers
* locale resolvers
* theme resolver
* multipart file resolver
* handler exception resolvers

当有一个请求到来的时候，DispatcherServlet是按照以下的顺序来处理这个请求的：

* 搜索WebApplicationContext，并且将其作为一个attribute绑定到request中，这样，在这个过程中，controller和其他的元素都可以使用。默认情况下，它被绑定在DispatcherServlet.WEB_APPLICATION_CONTEXT_ATTRIBUTE里面；
* locale resolver绑定到request中，这样，其他的元素可以解析并使用locale（呈现view、准备数据等等）。如果你不需要locale resolving，那么就不需要他它；
* theme resolver绑定到request中，允许views等元素决定使用哪个theme。如果不需要themes，可以忽略它；
* 如果指定了一个multipart file resolver，那么这个请求就被看做multipart。如果找到了multipart，就会将这个请求包装成一个MultipartHttpServletRequest，再由其它元素进行进一步的处理；
* 搜索一个合适的handler。如果找到了，那个和这个handler相关的执行链（preprocessors, postprocessors, and controllers）会被执行，以准备model以及呈现；
* 如果返回了一个model，那么会呈现一个view；如果没有model返回，那么不会呈现任何view，因为请求以及被执行完毕了。

