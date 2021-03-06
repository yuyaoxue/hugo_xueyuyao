---
title: "C# 中的访问修饰符和声明修饰符"
date: 2018-09-20T22:35:26+08:00
draft: false
---
# 前言

C# 中的访问修饰符和声明修饰符挺多的，总结一下，做个记录。

## 访问修饰符

访问修饰符通常作为声明字段数据类型的前缀，它标识了所修饰成员的封装级别。可以选择 5 个访问修饰符，即 public、private、protected、internal和 protected internal。

### public

公有的：显式指明可从类的外部访问被它修饰的字段。

### private

私有的：只有在声明它们的类和结构中才可以访问。如果不为类成员添加修饰符，那么默认使用的是 private。成员默认为私有成员，公共成员必须显式指定。

### protected

受保护的：可在基类中定义只有派生类才能访问的成员。

### internal

内部的，同一个程序集中的所有类都可以访问。

### protected internal

访问级别为 internal 或 protected。即，“同一个程序集中的所有类，以及所有程序集中的子类都可以访问。

## 声明修饰符

目前了解的声明修饰符有 8 个，即 partial、static、abstract、Sealed、Virtual、Override、New、Extern。

### Partial

在整个同一程序集中定义分部类和结构。

### Static

声明属于类型本身而不是属于特定对象的成员。

### Abstract

抽象类不可实例化，只能是其他类的基类。类中的方法只声明不实现，方法的实现在他的派生类中完成。其作用是强制所有派生类提供实现。

### Sealed

对类使用 sealed 修饰符可以禁止从该类继承。

### Virtual

用于修饰方法、属性、索引器或事件声明，并且允许在派生类中重写这些对象。

规则：虚方法只提供默认实现，这种实现可由派生类完全重写；“运行时”遇到虚方法时，他会调用虚成员派生得最远的，重写的实现。

### Override

提供从基类继承的成员的新实现。

### New

作为修饰符，在基类面前隐藏了派生类重新声明的成员，在不使用 new 修饰符的情况下隐藏成员是允许的，但会生成警告。作为运算符，用于创建对象和调用构造函数。

### Extern

用于声明在外部实现的方法。 extern 修饰符的常见用法是在使用 Interop 服务调入非托管代码时与 DllImport 特性一起使用。 在这种情况下，还必须将方法声明为 static。