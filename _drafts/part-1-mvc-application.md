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

{% responsive_image path: assets/images/microservices-tutorials/part-one/create-github-repository.png %}

Then clone the repository into your local machine. Copy the repository remote URL -

{% responsive_image path: assets/images/microservices-tutorials/part-one/clone-github.png %}

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

{% responsive_image path: assets/images/microservices-tutorials/part-one/visual-studio.png %}

### Create global.json file

Global.json file is used to select the correct .NET Core SDK version to build and run .NET Core application if you have multiple SDK version. You can see the list of installed SKDs in your machine by running -

```bash
dotnet --list-sdks
```

To work on .NET Core v 3.0, lets create a global.json file by running -

```bash
dotnet new globaljson --sdk-version 3.0.100
```

This also throw error if anyone try to build the code but do not have the specified version of SKD installed. It ensure the use of right SDK version.

### Create solution file

A solution is a structure for organizing projects in Visual Studio. Solution file itself doesn't do anything special. Although, you can build, run and deploy `.NET Core` application without the solution file, but having one make your projects much organized and easy to maintain. Although, we will only have one project at the beginning of this tutorial series, we will create and add more projects to the solution as we progress. 

```bash
dotnet new sln
```

### Create Project

Create folder for the project -

```bash
mkdir -p src/Web/WebMVC
```

This command will create three folder. Now create the `mvc` project -

```bash
dotnet new mvc --no-https -o src/Web/WebMVC
```

Here, `--no-https` tell the dotnet cli to generate scaffolding code without the **https** support and the `-o src/Web/WebMVC` argument set the output directory to `src>Web>WebMVC`.

Now lets add the project to the solution -

```bash
dotnet sln add src/Web/WebMVC
```

### Run the MVC Application

To configure `VSCode` to run the application, go to debug tab and click the setting icon marked in the screenshot bellow, then select `.NET Core`. Now you can run the application in **debug** mode by clicking the **run** button on pressing <kbd>F5</kbd> in your keyboard.

{% responsive_image path: assets/images/microservices-tutorials/part-one/vscode-debug-configure.png %}

After running application, you should see a webpage with the content similar to this -

{% responsive_image path: assets/images/microservices-tutorials/part-one/welcome-page.png %}


Congratulation, you have successfully created a `.NET Core MVC` web application. If you want to use **Visual Studio**, you can open the solution file (*.sln. For this tutorial `eCommerce-microservices-tutorial.sln` file) in Visual Studio and do the rest of the tutorial in Visual Studio too.  




