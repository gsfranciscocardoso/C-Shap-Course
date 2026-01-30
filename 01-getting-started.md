# Module 01: Getting Started with C#

## Overview

This module covers setting up your C# development environment and writing your first C# programs. As a PHP developer, you'll notice both familiar concepts and important differences.

## PHP vs C# Development Environment

| Aspect | PHP | C# |
|--------|-----|-----|
| **Runtime** | PHP interpreter | .NET Runtime (CLR) |
| **Compilation** | Interpreted (or JIT with OPcache) | Compiled to IL, then JIT to native code |
| **Package Manager** | Composer | NuGet |
| **Build Tool** | N/A (interpreted) | dotnet CLI / MSBuild |
| **Web Server** | Apache, Nginx, PHP built-in server | Kestrel, IIS |

## Installing the .NET SDK

### Windows
```bash
# Download from https://dot.net
# Or use winget
winget install Microsoft.DotNet.SDK.8
```

### macOS
```bash
brew install --cask dotnet-sdk
```

### Linux (Ubuntu/Debian)
```bash
wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
sudo apt-get update
sudo apt-get install -y dotnet-sdk-8.0
```

### Verify Installation
```bash
dotnet --version
```

## IDE Options

### Visual Studio Code (Recommended for PHP developers)
- Familiar if you use VS Code for PHP
- Install C# extension (powered by OmniSharp)
- Lightweight and cross-platform

### JetBrains Rider
- Similar to PhpStorm
- Excellent for PHP developers transitioning to C#
- Paid, but offers free trial

### Visual Studio
- Full-featured IDE (Windows/Mac)
- Free Community Edition available
- More heavyweight than VS Code

## Your First C# Program

### PHP Hello World
```php
<?php
// hello.php
echo "Hello, World!\n";
```

Run with: `php hello.php`

### C# Hello World
```csharp
// Program.cs
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello, World!");
    }
}
```

Or with modern C# (top-level statements):
```csharp
// Program.cs
Console.WriteLine("Hello, World!");
```

## Creating a C# Project

Unlike PHP where you just create a `.php` file, C# projects are structured:

```bash
# Create a new console application
dotnet new console -n HelloWorld

# Navigate to project
cd HelloWorld

# Run the application
dotnet run
```

### Project Structure
```
HelloWorld/
├── HelloWorld.csproj    # Project file (like composer.json)
├── Program.cs           # Main entry point
└── obj/                 # Build artifacts (like vendor/)
```

### Understanding .csproj (Project File)
```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>enable</Nullable>
  </PropertyGroup>
</Project>
```

**PHP Comparison**: Similar to `composer.json`, but for compilation settings and dependencies.

## Key Differences from PHP

### 1. Entry Point
**PHP**: Top-to-bottom execution of the file
```php
<?php
echo "This runs immediately";
```

**C#**: Explicit `Main` method (or top-level statements in modern C#)
```csharp
static void Main(string[] args)
{
    // Execution starts here
}
```

### 2. Compilation
**PHP**: Interpreted at runtime
```bash
php script.php  # Interprets and runs
```

**C#**: Compiled then executed
```bash
dotnet build    # Compiles to IL
dotnet run      # Runs the compiled code
```

### 3. Namespaces and Using
**PHP**: Namespaces with `\` separator
```php
<?php
namespace MyApp\Controllers;
use MyApp\Models\User;
```

**C#**: Namespaces with `.` separator
```csharp
namespace MyApp.Controllers;
using MyApp.Models;
```

## Basic Console I/O

### PHP
```php
<?php
// Output
echo "Hello";
print "World";

// Input
$name = readline("Enter your name: ");
echo "Hello, $name\n";
```

### C#
```csharp
// Output
Console.Write("Hello");      // No newline
Console.WriteLine("World");  // With newline

// Input
Console.Write("Enter your name: ");
string name = Console.ReadLine();
Console.WriteLine($"Hello, {name}");
```

## Comments

Both languages use similar comment syntax:
```csharp
// Single-line comment

/* 
   Multi-line comment
*/

/// <summary>
/// XML documentation comment (like PHPDoc)
/// </summary>
public void MyMethod() { }
```

## Reference Links

- [Install .NET SDK](https://dotnet.microsoft.com/download)
- [.NET CLI Overview](https://docs.microsoft.com/en-us/dotnet/core/tools/)
- [C# Introduction](https://docs.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/)
- [Visual Studio Code for C#](https://code.visualstudio.com/docs/languages/csharp)

## Exercises

### Exercise 1: Setup
1. Install the .NET SDK
2. Install VS Code with C# extension
3. Verify installation with `dotnet --version`

### Exercise 2: Hello, Your Name
Create a program that:
1. Asks for the user's name
2. Asks for their favorite programming language
3. Outputs: "Hello, [Name]! I see you like [Language]. Welcome to C#!"

**PHP Version** (for reference):
```php
<?php
$name = readline("What's your name? ");
$language = readline("Favorite language? ");
echo "Hello, $name! I see you like $language. Welcome to C#!\n";
```

**Your C# Task**: Implement this in C#.

### Exercise 3: Project Creation
1. Create a new console project called `MyFirstApp`
2. Modify it to print your name and current date
3. Build and run it using `dotnet` commands

### Exercise 4: Exploration
1. Examine the `.csproj` file
2. Find where the build output goes (look in `bin/` folder)
3. Compare the project structure to a typical PHP project

## Solutions

Solutions can be found in [/exercises/01-getting-started/](./exercises/01-getting-started/)

---

**Next Module**: [02 - Syntax Comparison](./02-syntax-comparison.md)