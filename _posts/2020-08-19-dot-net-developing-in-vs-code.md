---
layout: post
title:  ".NET developing in Visual Studio Code"
categories: posts
tags: vscode, dotnet, dotnetcore, razor, razorpages
---
## Basic shortcuts

| **Shortcut** | **Function** |
| --- | --- |
| ``Ctrl + ` `` | Opens the console |
| ``Ctrl + Shift + E`` | Opens the explorer |
| ``Ctrl + Shift + F`` | Search panel |
| ``Ctrl + Shift + D`` | Debugging panel |
| ``Ctrl + B`` | Opens and closes the sidebar |
| ``Ctrl + ,`` | Settings |
| ``Ctrl + p`` | File search |
| ``Ctrl + Shift + P`` | Command palette |
| ``Ctrl + W`` | Closes the current window |
| ``Ctrl + S`` | Saves the current window |



## Basic terminal commands

| **Shortcut** | **Function** |
| --- | --- |
| ``code .`` | Opens VS Code in the current folder |
| ``code . --locale=fr`` | As above, but with language settings |
| ``clear`` | Clears the terminal window |
| ``type FILE`` | Shows the FILE content |
| ``dir`` | Lists the content of the current folder |
| ``dir FOLDER`` | Lists the content of the FOLDER |
| ``dir ..`` | Lists the content of the higher folder |



## .NET CLI (Command-Line Interface) general commands

| **Command** | **Function** |
| --- | --- | 
| ``dotnet --version`` | Check the .NET version |
| ``where dotnet`` | Shows the location of .NET files (only on Windows) |
| ``dotnet -h``, ``dotnet --help`` | General help on .NET CLI commands |



## Project templates

| **Command** | **Function** |
| --- | --- |
| ``dotnet new -h`` | Help on project templates |
| ``dotnet new -l`` | Lists all available templates |
| ``dotnet new TEMPLATE -o NAME`` | Creates a project named NAME based on TEMPLATE |
| ``dotnet new TEMPLATE -n NAME -O FOLDER -f FRAMEWORK`` | As above but with location folder and project framework specified |


Example: 

```bash
dotnet new classlib o- MyClass -f netcoreapp3.1
```


## Project names


### Console apps and libraries

| **Short Name** | **Default framework**[^fr] | **Project** | **Languages**[^lang] |
| --- | --- | --- |
| ``console`` | .NET Core 3.1 | Console application | C#, F#, VB |
| ``classlib`` | .NET Core 2.0! | Class library | C#, F#, VB |


### WPF applications

| **Short Name** | **Default framework**[^fr] | **Project** | **Languages**[^lang] |
| --- | --- | --- |
| ``wpf`` | .NET Core 3.1 | WPF application | C# |
| ``wpflib`` | .NET Core 3.1 | WPF class library | C# |
| ``wpfcustomcontrollib`` | n.a. | custom controll library[^contr_lib] | C# |
| ``wpfusercontrollib`` | n.a. | user controll library[^contr_lib] | C# |


### Window Forms

| **Short Name** | **Default framework**[^fr] | **Project** | **Languages**[^lang] |
| --- | --- | --- |
| ``winforms`` | .NET Core 3.1 | WinForms application | C# |
| ``winformslib`` | .NET Core 3.1 | WinForms class library | C# |


### Server apps

| **Short Name** | **Default framework**[^fr] | **Project** | **Languages**[^lang] |
| --- | --- | --- |
| ``worker`` | .NET Core 3.1 | Worker Service[^work] | C# |
| ``web`` | .NET Core 3.1 | ASP.NET Core empty | C#, F# |
| ``webapi`` | .NET Core 3.1 | ASP.NET Core web API | C#, F# |
| ``mvc`` | .NET Core 3.1 | ASP.NET Core MVC web application | C#, F# |
| ``webapp`` | .NET Core 3.1 | ASP.NET Core Razor Pages web application | C# |
| ``razorclasslib`` | .NET Standard 2.0[^st] | Razor class library | C# |


### Web app views

| **Short Name** | **Default framework**[^fr] | **Project** | **Languages**[^lang] |
| --- | --- | --- |
| ``razorcompontent`` | n.a. | Razor component (.razor file) | C# |
| ``page`` | n.a. | Razor page (.cshtml and .cshtml.cs files) | C# |
| ``viewimports`` | n.a. | MVC ViewImports | C# |
| ``viewstart`` | n.a. | MVC ViewStart | C# |


### Blazor apps

| **Short Name** | **Default framework**[^fr] | **Project** | **Languages**[^lang] |
| --- | --- | --- |
| ``blazorserver`` | .NET Core 3.1 | Blazor server application | C# |
| ``blazorwasm`` | .NET Standard 2.1[^st] | Blazor WebAssembly application | C# |


### Tests

| **Short Name** | **Default framework**[^fr] | **Project** | **Languages**[^lang] |
| --- | --- | --- |
| ``mstest`` | .NET Core 3.1 | Unit test project | C#, F#, VB |
| ``nunit`` | .NET Core 3.1 | NUnit 3 test project | C#, F#, VB |
| ``nunit-test`` | n.a. | NUnit 3 test class | C#, F#, VB |
| ``xunit`` | .NET Core 3.1 | xUnit test project | C#, F#, VB |


### Other files

| **Short Name** | **Default framework**[^fr] | **Project** | **Languages**[^lang] |
| --- | --- | --- |
| ``sln`` | n.a. | Solution file (.sln) | n.a. |
| ``gitignore`` | n.a. | .NET gitignore file | n.a. | 
| ``webconfig`` | n.a. | Web config file | n.a. |
| ``globaljson`` | n.a. | global.json file | n.a. |
| ``tool-manifest`` | n.a. | dotnet-tools.json file | n.a. |
| ``nugetconfig`` | n.a. | NuGet config file (nuget.config) | n.a. |


[^lang]:For every template the default language is C#. 

[^fr]:To change the framework to .NET Framework, change the ``Target Framework`` value in ``.csproj`` file to ``net45`` or ``net47`` (conf. [How to create a .net framework class library in new .csproj formate #9208](https://github.com/dotnet/sdk/issues/9208)).

[^contr_lib]:On the difference between custom controll library and user control library see [What is the difference between a User Control Library and a Custom Control Library?](https://stackoverflow.com/questions/807703/what-is-the-difference-between-a-user-control-library-and-a-custom-control-libra).

[^work]:On worker services see [Worker Service in .NET Core 3.1](https://wakeupandcode.com/worker-service-in-net-core-3-1/) and [Background tasks with hosted services in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/host/hosted-services?view=aspnetcore-3.1&tabs=visual-studio&WT.mc_id=-blog-shchowd#worker-service-template).

[^st]:On .NET Standard see [.NET Standard](https://docs.microsoft.com/en-gb/dotnet/standard/net-standard).

Source: [dotnet new](https://docs.microsoft.com/en-gb/dotnet/core/tools/dotnet-new)



## Building, starting and publishing

| **Command** | **Function** |
| --- | --- |
| ``dotnet build .\FOLDER\PROJECT.csproj`` | Builds the project |
| ``dotnet run`` | Runs the project in the current folder |
| ``dotnet run -p .\FOLDER\PROJECT.csproj`` | Runs the project in the folder specified |
| ``dotnet run --p .\FOLDER\PROJECT.csproj`` | As above |
| ``dotnet publish .\FOLDER\PROJECT.csproj -o ..\build -c Release`` | Publishes the project in build folder of the main folder |



## References

| **Command** | **Function** |
| --- | --- |
| ``dotnet add .\FOLD\Proj1.csproj reference .\FOLD\Proj2.csproj`` | In Proj1 adds reference to Proj2 |
| ``dotnet add .\FOLD\PROJ.csproj reference .\F1\P1.csproj .\F2\P2.csproj`` | Adds several references in PROJ |
| ``dotnet list reference`` | Lists all reference of the project in the current folder |
| ``dotnet list .\FOLD\PROJ.csproj reference`` | As above, but with folder location specified |
| ``dotnet remove .\F1\Proj1.csproj reference .\F2\Proj2.csproj`` | Removes the reference to Proj2 in Proj1 |
| ``dotnet remove .\FOLD\PROJ.csproj reference .\F1\P1.csproj .\F2\P2.csproj`` | Removes several references |



## NuGet packages

| **Command** | **Function** |
| --- | --- |
| ``dotnet add package PACK`` | Adds PACK package to the current project |
| ``dotnet add PROJ.csproj package PACK -v 1.0.0`` | Adds PACK of given version to PROJ |
| ``dotnet add package PROJ -s SITE`` | Adds package from a particular site |
| ``dotnet list package`` | Lists all packages in the current project |
| ``dotnet list PROJ.csproj package`` | Lists all packages in the PROJ project |
| ``dotnet list --outdated --include-prerelease`` | Lists only outdated and beta-version packages |
| ``dotnet list package --framework netcoreapp3.0`` | Lists only .NET Core 3.0 packages |
| ``dotnet remove package PACK`` | Removes the PACK package |
| ``dotnet pack .\FOLD\PROJ.csproj`` | Creates a NuGet package out of the project |

Examples:

```bash
dotnet add package MongoDb.Driver.Core --version 2.10.0

dotnet add package Microsoft.AspNetCore.StaticFiles -s https://dotnet.myget.org/F/dotnet-core/api/v3/index.json
```


## Solutions

| **Command** | **Function** |
| --- | --- |
| ``dotnet new sln -o NAME`` | Creates solution of the given name |
| ``dotnet new sln -n NAME -O FOLDER`` | As above but in the folder specified |
| ``dotnet new sln -h`` | Help on solution commands |
| ``dotnet sln SOL.sln add .\F1\P1.csproj .\F2\P2.csproj`` | Adds P1 and P2 to SOL solution |



## Tests

| **Command** | **Function** |
| --- | --- |
| ``dotnet new TEST_SHORT_NAME -o NAME`` | Creates new unit test |
| ``dotnet test .\FOLD\TEST.csproj`` | Runs all tests in the TEST project |
| ``dotnet test --filter "FullyQualifiedName=NAMESPACE.TESTCLASS.TESTMETHOD`` | Runs a particular test |
| ``dotnet test xunit -method FullyQualifiedName`` | As above, but xUnit test |

Test short names

| **Test short name** | **Test type** |
| --- | --- |
| ``mstest`` | Microsoft unit test |
| ``nunit`` | NUnit test |
| ``xunit`` | xUnit test |



## Sources

[dotnet new](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-new?tabs=netcore22)

[dotnet build](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-build)

[Display Language](https://code.visualstudio.com/docs/getstarted/locales)

[How to change UI language in Visual Studio Code](https://stackoverflow.com/questions/36868322/how-to-change-ui-language-in-visual-studio-code)

[Create C# .sln file with Visual Studio Code](https://stackoverflow.com/questions/36343223/create-c-sharp-sln-file-with-visual-studio-code)

[How to use .NET Core CLI to Create a Multi-Project Solution](https://www.skylinetechnologies.com/Blog/Skyline-Blog/February_2018/how-to-use-dot-net-core-cli-create-multi-project)

[Add Class Library In ASP.NET Core using .NET Core Command-Line Interface (CLI)](https://www.c-sharpcorner.com/article/add-class-library-in-asp-net-core-using-net-core-command-line-interface-cli/)

[dotnet remove package](https://docs.microsoft.com/pl-pl/dotnet/core/tools/dotnet-remove-package)

[MongoDB.Driver.Core](https://www.nuget.org/packages/MongoDB.Driver.Core/)

[How do I run specific tests using dotnet test?](https://stackoverflow.com/questions/37752273/how-do-i-run-specific-tests-using-dotnet-test)


