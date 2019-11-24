---
layout: single
title: "Part one: Getting started with asp.net core MVC"
categories:
    - Microservices
comments: true
toc: true
---
Today, we will create a basic ASP.NET Core MVC web application. But before that lets create a github repository for our project

## Create & Clone GitHub repository
At first lets create a GitHub repository. To create a GitHub repository you can use the new `.new` domain [repo.new](https://repo.new). Don't forget to select `Visual Studio` **.gitignore**, because we don't want to commit `Visual Studio` generated build artifacts and user specific configurations into `git`.

{% responsive_image path: assets/images/microservices-tutorials/create-github-repository.png %}

Then clone the repository into your local machine. Copy the repository remote URL -

{% responsive_image path: assets/images/microservices-tutorials/clone-github.png %}

and then run the command -

```bash
git clone <your repository URL>
```

For my repository, the command is -

```bash
git clone git@github.com:ratanparai/eCommerce-microservices-tutorial.git
```

## Setup initial project structure

