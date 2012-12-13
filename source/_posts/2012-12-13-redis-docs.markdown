---
layout: post
title: Redis文档
date: 2012-12-13 09:27
comments: true
categories: [redis]
---
###1. Redis介绍
####1.1 什么是redis
REmote DIctionary Server(Redis)是一个由Salvatore Sanfilippo写的key-value存储系统。Redis提供了一些丰富的数据结构，包括lists，sets，ordered sets以及hashes，当然还有和Memcached一样的strings结构。Redis当然还包括了对这些数据结构的丰富操作。

####1.2 redis的优点
* 性能极高：Redis能支持超过 100K+ 每秒的读写频率；
* 丰富的数据类型：Redis支持二进制安全的Strings，Lists，Hashes，Sets及Ordered Sets数据类型操作；
* __原子性：Redis的所有操作都是原子性的，同时Redis还支持对几个操作全并后的原子性执行；__
* 丰富的特性：Redis还支持 publish/subscribe，通知，key过期等等特性。

<!-- more -->

###2. Redis的数据类型
redis使用的是key作为存取对象的唯一标识，对“key”的通俗理解就是“字符串”。在Redis中字符串又分为两类：二进制安全(Binary Safe)的和非二进制安全的，关于二进制安全的描述可以参考[binary safe](http://en.wikipedia.org/wiki/Binary_safe)。Redis处理存储的内容时用的是二进制安全的字符串，而作为key使用的非二进制安全的。

####2.1 String
#####2.1.1 String的结构
redis string的实现包含在sds.c文件中，redis string的定义在sdshdr.h文件中：

```
struct sdshdr {
    long len;
    long free;
    char buf[];
};
// len代表buf中实际保存的字符串的长度，那么就可以再O(1)的时间内获取字符串的长度
// free代表buf中还剩余的空间长度
// 保存实际的字符串
// len + free 等于buf数组的长度
```

#####2.1.2 String的创建
在sds.h中定义了一个新的类型，实际上类型sds就是字符串指针的一个别名而已。

```
typedef char *sds;
```

在sds.c中定义的sdsnewlen函数创建一个新的字符串：

```
sds sdsnewlen(const void *init, size_t initlen) {
    struct sdshdr *sh;

    sh = zmalloc(sizeof(struct sdshdr)+initlen+1);
#ifdef SDS_ABORT_ON_OOM
    if (sh == NULL) sdsOomAbort();
#else
    if (sh == NULL) return NULL;
#endif
    sh->len = initlen;
    sh->free = 0;
    if (initlen) {
        if (init) memcpy(sh->buf, init, initlen);
        else memset(sh->buf,0,initlen);
    }
    sh->buf[initlen] = '\0';
    return (char*)sh->buf;
}
```

可以看到，函数介绍两个参数，一个是字符串指针，一个是字符串长度。然后分配一个地址空间，包括三个部分：struct sdshdr长度、字符串长度以及字符串最后的结尾符。最后对struct sdshdr的各个元素赋值，返回其buf部分，也就是实际的字符串。

假设使用如下代码初始化它，那么内存结构大概是下面这个样子的：

```
// 初始化
sdsnewlen("bd17kaka", 8);

// 结果
-----------
|8|0|bd17kaka|
-----------
^   ^
sh  sh->buf

```

#####2.1.3 通过buf指针获取sh指针
从上面的内存结构图可以看到，buf的内存地址实际上只比sh的内存地址多了len和free两个变量的长度，也就是两个long的长度，实际上就是struct sdshdr的长度，那么可以通过以下方法获取sh的指针：

```
struct sdshdr *sh = (void*) (s-(sizeof(struct sdshdr)));

// 获取字符串的长度
size_t sdslen(const sds s) {
    struct sdshdr *sh = (void*) (s-(sizeof(struct sdshdr)));
    return sh->len;
}
```

在redis源代码其他地方，可以经常看到这个技巧的使用。


####2.2 List


####2.3 set（集合）


####2.4 sorted set（有序集合）


####2.5 hash


###3. Publish/Subscribe


###4. 数据过期


###5. 事务性


###6. 持久化


###7. 管理