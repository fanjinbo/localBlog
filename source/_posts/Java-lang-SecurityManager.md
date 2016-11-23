---
title: Java.lang.SecurityManager
date: 2016-11-23 17:45:58
tags: Java学习
---
## jdk文档定义

安全管理器是一个允许应用程序实现安全策略的类。它允许应用程序在执行一个可能不安全或敏感的操作前确定该操作是什么，以及是否是在允许执行该操作的安全上下文中执行它。应用程序可以允许或不允许该操作。

SecurityManager 类包含了很多名称以单词 check 开头的方法。Java 库中的各种方法在执行某些潜在的敏感操作前可以调用这些方法。对 check 方法的典型调用如下：

     SecurityManager security = System.getSecurityManager();
     if (security != null) {
         security.checkXXX(argument,  . . . );
     }

因此，安全管理器通过抛出异常来提供阻止操作完成的机会。如果允许执行该操作，则安全管理器例程只是简单地返回，但如果不允许执行该操作，则抛出一个 SecurityException。该约定的唯一例外是 checkTopLevelWindow，它返回 boolean 值。

    getSecurityManager
    public static SecurityManager getSecurityManager(){
          return security;
    }


获取系统安全接口。

返回：
如果已经为当前应用程序建立了安全管理器，则返回此安全管理器；否则，返回 null。