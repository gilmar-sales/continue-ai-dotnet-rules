---
globs: ./**/*
description: This rule ensures consistency in handling .NET development tasks by
  suggesting appropriate CLI commands and reminding about correct directory
  contexts for executing tools like 'nuget install'. Apply it when discussing
  project creation, dependency management, or other .NET-related code generation
  to follow best practices from the dotnet CLI documentation.
alwaysApply: false
---

Always use .NET Core CLI commands such as 'dotnet new {template} -n {name}' to create projects with specific templates like class, classlib, webapi or webapi-minimal. Additionaly when using the classlib template you should remove the Class1.cs file from the project dir. For adding project references between components (e.g., libraries and applications), specify the command format including all required parameters in your code suggestions. Additionally, ensure that any NuGet package installation commands are noted as needing execution within the directory containing the relevant .NET project files.
