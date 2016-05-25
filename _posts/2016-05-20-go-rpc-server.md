---
layout: post
title:  How to build RPC server in golang (step by step with examples)
description: ""
category: articles
tags: [golang, go, rpc, rpc server, remote procedure call, RPC]
comments: true
---

# Overview

[Remote procedure call](https://en.wikipedia.org/wiki/Remote_procedure_call) (RPC) is basically a form of inter-process communication. It is widely used in distributed computing.

In this blog post, We will build a simple RPC server step by step.

## 1. Define an interface and shared structs
For sake of simplicity, we will choose an interface with two methods: `Multiply` and `Divide`, which perform `*` and `/` operations respectively.

There will be only two shared structs called `Args`, and `Quotient` that will be used to pass arguments from client to server and represent the output of divide, respectively.

{% gist b22355ff4877f712ded4d1c1cd08e488 %}
{% gist 81158f3b12ca1e0cdb7becbe40be3c2f %}


## 2. Write implementation for the interface
Now, we will write struct which implements two method we mentioned above: `Multiply` and `Divide`.

{% gist  ca422ce77052ed1b646876f6c70a555a %}

## 3. Implement a RPC server
Two ways we can implement a RPC server in golang:

### 3.1 HTTP RPC
In this case server will be listening for incoming connection using HTTP protocol, and will switch to RPC protocol afterwards.

Benefit of this approach is, you can perform authentication of client easily, before allowing RPC, using any authentication method supported by HTTP.

{% gist 8dd78fd13ba84cc2d1e2ff503ae7e44a %}

Internally, server listens for HTTP `CONNECT` method, and then uses `http.Hijacker` to hijack the connection.

### 3.2 TCP RPC
In this case server will be listening for incoming connection directly, instead of relying on HTTP protocol.

{% gist 84d368c64721541eee1d3379ad7ae916 %}

## 4. Implement a RPC client
We need to implement RPC client, based on which way we chose to build our server.

### 4.1 HTTP RPC

{% gist f81afbc9c0490a3edcab58abc2d215f0 %}

### 4.2 TCP RPC

{% gist a85c7d1f46cd6620969c940ad39a6239 %}
