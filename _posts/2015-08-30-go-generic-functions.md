---
layout: post
title:  Design generic function in golang, with help of functional programming and reflection
description: ""
category: articles
tags: [golang, go, functional programming, reflection, reflect]
comments: true
---

Overview
========
Starting from golang 1.1, it offers reflection support to do almost anything dynamically. Combine that with functional programming support, and you can write generic functions in no time.

In this article, I will describe how to write generic functions in golang, as well as pros and cons of the same.

Functional Programming in Golang
--------------------------------
Golang supports first class functions, higher-order functions, user-defined function types, function literals, closures, and multiple return values. 

For scope of this article, I will demonstrate three of above features: function literals, function types and higher order functions.

{% gist 52cb0e477270600b5383 %}

In this example, we implemented `filterArray` function, that takes two arguments, array of integer and a function. And filter the array using the function passed.

As you can see, we call `filterArray` function, two times with different function literal, first literal filters out odd numbers, while second removes even numbers.

But, this is not enough to write truly generic code, as you can see, we can only pass integer array and only functions who are compatible with function type that we declared beforehand. 

Enter reflection!!

Reflection in Golang 
--------------------
Unlike C/C++, in golang every object retains associated type information, even if it is assigned to a `interface` variable. This plays key part, while using reflection.

Reflection apis are exposed in golang, through built-in package called `reflect`.















