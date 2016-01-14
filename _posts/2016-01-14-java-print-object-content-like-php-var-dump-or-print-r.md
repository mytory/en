---
title: Java, print Object content like php var_dump or print_r using Pojomatic
author: Ahn, Hyeong-woo
layout: post
categories:
  - serverside
tags:
  - java, pojomatic
---

I've been PHP developer. PHP has powerful debug method like `print_r`, `var_dump` and debug lib like [xdebug](http://xdebug.org/).

But, as JAVA developer I'm troubled with absence of debug method. 

Although inconvenient, you can use a `toString()` method like `print_r` in JAVA. It is [Pojomatic library](http://www.pojomatic.org/).

If you use maven, add dependency to `pom.xml`.

    <dependency>
        <groupId>org.pojomatic</groupId>
        <artifactId>pojomatic</artifactId>
        <version>1.0</version>
    </dependency>


Then, import Pojomatic and add `@AutoProperty` annotation to class you want to read like `PostVo.java`.

    import org.pojomatic.Pojomatic;
    import org.pojomatic.annotations.AutoProperty;

    @AutoProperty
    public class PostVO { ... }

And, override toString method like this:

    @Override
    public String toString() {
        return Pojomatic.toString (this);
    }

You can override `hashCode()` and `equals(Object o)`.

    @Override
    public boolean equals(Object o) {
        return Pojomatic.equals (this, o);
    }

    @Override
    public int hashCode() {
        return Pojomatic.hashCode (this);
    }

You can use below code, and see below result.

    System.out.println(new Person("John", "Doe", 32).toString());
    
    // result: Person{firstName: {John}, lastName: {Doe}, age: {32}}

Of course, you can use code like `logger.debug("{}", vo)`.