---
layout: single
title: "Part two: Getting started with asp.net core MVC"
date: 2019-12-14T18:57:53+06:00
last_modified_at: 2019-12-14T18:57:56+06:00
categories:
    - Microservices
comments: true
tags: 
    - microservices
    - dotnet core
toc: true
---

CRUD to DDD

## Automatic Migrations

In the previous tutorial, we have to apply migration by manually running the command `dotnet ef database update`. We need to do this automatically in container environment. We can run the migration programmatically by calling `{DBContext}.Database.Migrate()`, where `{DBContext}` is instance of our `DBContext` class (In our case instance of `CatalogContext` class).

```cs
using var scope = host.Services.CreateScope();

var services = scope.ServiceProvider;

var context = services.GetService<TContext>();
var logger = services.GetRequiredService<ILogger<TContext>>();
```


## Seed data

## Basket Domain

## Introduce Service

## CRUD vs DDD

## Domain Model

## Modify View for Domain


