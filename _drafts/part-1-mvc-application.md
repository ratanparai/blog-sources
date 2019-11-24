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

Open the locally cloned repository folder in `VSCode` and open the `VSCode` (Check [VSCode Integrated Terminal](https://code.visualstudio.com/docs/editor/integrated-terminal) for more info) terminal window. The rest of today's tutorial we will use the `VSCode` terminal and `dotnet` command line to tool to setup the initial structure and projects.

You should see similar to this window-

{% responsive_image path: assets/images/microservices-tutorials/visual-studio.png %}

### Create global.json file

Global.json file is used to select the correct .NET Core SDK version to build and run .NET Core application if you have multiple SDK version.

```bash
dotnet new globaljson --sdk-version 3.0.100
```

### Create solution file

<!-- TODO:  Write why we need solution file here -->

```bash
dotnet new sln
```

### Create Projects




