---
layout: single
title: RabbitMQ messaging between two Java Springboot application
categories:
    - Microservice
comments: true
tags:
    - java
    - springboot
    - rabbitmq
toc: true
---

In this blog post I am going to discuss about how to send message between two java spring boot application using RabbitMQ message broker. 

## Prerequisite
1. Install [JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html){:target="_blank"}
3. Install [maven](https://maven.apache.org/){:target="_blank"}
2. Install Visual Studio Code (Optional)

## Create initial spring boot applicaiton(two)
From [Spring Initializr](https://start.spring.io/) website generate two project with `Web` and `RabbitMQ` dependencies. 

{% responsive_image path: assets/images/generate-spring-boot-maven-project.png %}

## Write message publisher

**Please note:** exhange that work as direct and fanout exchange depending on bindings
{: .notice--danger}

## Write message receiver



