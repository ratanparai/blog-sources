In ASP.NET core 2.1, setting up functional testing project got much easier with the release of [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) nuget package. In this post we are going to setup a functional test project.

## Create test project
Create a folder and name it `HelloWorld`, because why not :stuck_out_tongue_winking_eye:. Open **PowerShell** window inside the folder (<kbd>Shift</kbd> + `right click` anywhere inside the folder and select `Open PowerShell window here`) and create a solution:

```bash
dotnet new sln
```

Now create a basic **MVC** project inside `src` directory and **xunit** project inside `tests` directory:

```bash
dotnet new mvc -o .\src\HelloWorld.Mvc
dotnet new xunit -o .\tests\HelloWorld.FunctionalTests
```

Add those two project to the **solution**:

```bash
dotnet sln add .\src\HelloWorld.Mvc\HelloWorld.Mvc.csproj
dotnet sln add .\tests\HelloWorld.FunctionalTests\HelloWorld.FunctionalTests.csproj
```

Reference the **MVC** project form the **FunctionalTests** project:

```bash
dotnet add .\tests\HelloWorld.FunctionalTests\HelloWorld.FunctionalTests.csproj reference .\src\HelloWorld.Mvc\HelloWorld.Mvc.csproj
```

Add [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) to the functional test project:

```bash
dotnet add .tests\HelloWorld.FunctionalTests\HelloWorld.FunctionalTests.csproj package Microsoft.AspNetCore.Mvc.Testing -v 2.1.0-rc1-final
```

Now open the project in **VS Code** or **>= Visual Studio 2017 x.x.x** and create a new class inside **HelloWorld.FunctionalTests** project and name it `HomePageShould.cs`


