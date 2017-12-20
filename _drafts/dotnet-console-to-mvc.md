# Create dotnet console app

```bash
dotnet new console
```

this will create **dotnet core** console application. There should be two file `[projectName].csproj` and `Program.cs`, where `[projectName]` is the name of the working folder. Lets look at the content of those two files

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.0</TargetFramework>
  </PropertyGroup>

</Project>
```

and the `Program.cs` file is

```csharp
using System;

namespace console
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

you can run the application by running `dotnet run` in terminal/console. this will output -

```
Hello World!
```

## Install aspnetcore

```bash
dotnet add package Microsoft.AspNetCore.All
```

This will install all required component of `AspNetCore` framework.

## Modify `Program.cs` file

we are going add minimum line of codes to make this a web app. Create a new class file with any name you want, I am using `Start.cs` (You can use anything you want)

```csharp
using Microsoft.Extensions.Configuration;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;

namespace console
{
    public class Start
    {
        public void Configure(IApplicationBuilder app)
        {
            app.Run(async context => await context.Response.WriteAsync("Hello World"));
        }
    }
}

```

and the `Program.cs` file

```csharp
using System;
using Microsoft.AspNetCore;
using Microsoft.AspNetCore.Hosting;

namespace console
{
    class Program
    {
        static void Main(string[] args)
        {
            WebHost.CreateDefaultBuilder()
                .UseStartup<Start>()
                .Build()
                .Run();
        }
    }
}

```

## Deploy

Add -

```xml
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.0</TargetFramework>
    <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
  </PropertyGroup>
```

now run

```bash
dotnet publish -c Release -r win10-x64
```

List of runtime identifiers can be found in [.NET Core RID Catalog](https://docs.microsoft.com/en-us/dotnet/core/rid-catalog)

**Please Note:** Read more about [.NET Core application deployment](https://docs.microsoft.com/en-us/dotnet/core/deploying/)
{: .notice--danger }