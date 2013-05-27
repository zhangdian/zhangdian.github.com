---
layout: post
title: "Spring WEB MVC总结"
date: 2013-05-27 00:26
comments: true
categories: [spring,java,web,mvc]
---

用了这么久的spring web，终于把官方的文档看了看，总结出来下面的文档。

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

