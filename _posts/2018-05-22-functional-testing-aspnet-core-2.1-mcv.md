---
layout: single
title: Functional Testing of ASP.NET core 2.1 MVC Application
date: 2018-05-22 21:00:00 +0600
categories:
    - dotnet
tags:
    - asp.net core
    - functional testing
    - dotnet core
excerpt: In ASP.NET core 2.1, setting up functional testing project got much easier with the release of [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) nuget package. 
comments: true
---

In ASP.NET core 2.1, setting up functional testing project got much easier with the release of [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) nuget package. In this post we are going to setup a functional test project.

## Prerequisite

To follow this tutorial you should have-

1. [.NET Core 2.1 RC1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-rc1) and
2. [VS Code](https://code.visualstudio.com/) or [Microsoft Visual Studio 2017](https://www.visualstudio.com/downloads/) v15.7 Preview 1 or newer, installed on your system

## Create test project
Create a folder and name it `HelloWorld`, because why not :stuck_out_tongue_winking_eye:. Open **PowerShell** window inside the folder (<kbd>Shift</kbd> + `right click` anywhere inside the folder and select `Open PowerShell window here`) and create a solution:

```
dotnet new sln
```

Now create a basic **MVC** project inside `src` directory and **xunit** project inside `tests` directory:

```
dotnet new mvc -o .\src\HelloWorld.Mvc
dotnet new xunit -o .\tests\HelloWorld.FunctionalTests
```

Add those two project to the **solution**:

```
dotnet sln add .\src\HelloWorld.Mvc\HelloWorld.Mvc.csproj
dotnet sln add .\tests\HelloWorld.FunctionalTests\HelloWorld.FunctionalTests.csproj
```

Reference the **MVC** project form the **FunctionalTests** project:

```
dotnet add .\tests\HelloWorld.FunctionalTests\HelloWorld.FunctionalTests.csproj reference .\src\HelloWorld.Mvc\HelloWorld.Mvc.csproj
```

## Write functional Test

Add [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) to the functional test project:

```
dotnet add .\tests\HelloWorld.FunctionalTests\HelloWorld.FunctionalTests.csproj package Microsoft.AspNetCore.Mvc.Testing -v 2.1.0-rc1-final
```

Now open the project in **VS Code** or **Visual Studio 2017 15.7 Preview 1 or newer** and create a new class inside **HelloWorld.FunctionalTests** project and name it `HomePageShould.cs`

```csharp
using HelloWorld.Mvc;
using Microsoft.AspNetCore.Mvc.Testing;
using System.Net;
using System.Net.Http;
using System.Threading.Tasks;
using Xunit;

namespace HelloWorld.FunctionalTests
{
    public class HomePageShould : IClassFixture<WebApplicationFactory<Startup>>
    {
        private readonly HttpClient _client;

        public HomePageShould(WebApplicationFactory<Startup> factory)
        {
            _client = factory.CreateClient();
        }

        [Fact]
        public async Task ReturnHttpStatusCodeOk()
        {
            var response = await _client.GetAsync("/");

            Assert.Equal(HttpStatusCode.OK, response.StatusCode);
        }
    }
}
```

## Run the test

Now run the **test**. It should fail with the error message

> Message: System.IO.FileNotFoundException : Could not load file or assembly 'Microsoft.AspNetCore, Version=2.1.0.0, Culture=neutral, PublicKeyToken=adb9793829ddae60'. The system cannot find the file specified.

To resolve it, add [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) nuget package to the **test** project

```
dotnet add .\tests\HelloWorld.FunctionalTests\HelloWorld.FunctionalTests.csproj package Microsoft.AspNetCore.App -v 2.1.0-rc1-final
```

Now run the test from `Test`>`Run`>`All Tests` (Visual Studio 2017) or from **PowerShell**-

```
dotnet test .\tests\HelloWorld.FunctionalTests\HelloWorld.FunctionalTests.csproj
```

You should see green tick of happiness.


