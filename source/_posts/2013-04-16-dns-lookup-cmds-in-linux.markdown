---
layout: post
title: "linux上常见DNS记录查询"
date: 2013-04-16 09:40
comments: true
categories: [mail,邮件]
---

首先介绍一个查询DNS记录很好的网站：[MXToolBox](http://mxtoolbox.com/SuperTool.aspx)

查询DKIM记录：dig TXT + short mail._domainkey.domain.com

查询SPF记录：dig TXT +short domain.com

查询MX记录：dig MX domain.com

查询A记录：dig A domain.com