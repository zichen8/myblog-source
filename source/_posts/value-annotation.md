---
layout: page
categories: "code"
title:  "注解"
tags: [java,lombok,redisson]
date: 2020-07-16
---
在java类中用@Value注解，读取application.yml的属性，并绑定变量，代码如下<!--more-->

```
    @Value("${myjwt.tokenExpireTime}")
    public Integer tokenExpireTime;

```
<br>
application.yml
```
myjwt:
  tokenExpireTime: 1024
```

用Alt+Enter键自动引用了 “lombok.Value” 包，结果@Value这行标注红字，编译无法通过。

后来在网上搜到问题所在，此时要导入的Value的包不是lombok.Value,而是org.springframework.beans.factory.annotation.Value，
更换了导入包，则问题解决。

lombok里@Value的用法：注解在类上，相当于为属性添加 final 声明，只提供 getter 方法，而不提供 setter 方法。

Java的一个“暴力”美学之处在于注解，可省略很多重复性的代码。在方法上加注解可以实现很多复杂功能，并且方法内部无代码侵入，比如Redisson的分布式锁，
最近在学习[redisson-spring-boot-starter](https://gitee.com/ztp/redisson-spring-boot-starter)，开源软件，支持多种上锁方式，
注解是@Lock。
