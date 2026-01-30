# Module 04: OOP Fundamentals - Classes and Objects in C#

## Overview

As a PHP developer, you're already familiar with OOP concepts. This module explores how C# implements OOP, highlighting both similarities and key differences from PHP. C# is a pure object-oriented language where everything is part of a class.

## Table of Contents
1. [Classes and Objects](#classes-and-objects)
2. [Properties vs Fields](#properties-vs-fields)
3. [Methods](#methods)
4. [Constructors](#constructors)
5. [Access Modifiers](#access-modifiers)
6. [Namespaces](#namespaces)
7. [Static Members](#static-members)
8. [The `this` Keyword](#the-this-keyword)
9. [Object Initialization](#object-initialization)

---

## Classes and Objects

### PHP Class Definition
```php
<?php
class Person 
{
    public $name;
    public $age;
    
    public function __construct($name, $age) 
    {
        $this->name = $name;
        $this->age = $age;
    }
    
    public function introduce() 
    {
        return "Hi, I'm {$this->name} and I'm {$this->age} years old.";
    }
}

$person = new Person("John", 30);
echo $person->introduce();
```

### C# Class Definition
```csharp
using System;

public class Person
{
    private string name;
    private int age;
    
    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }
    
    public string Introduce()
    {
        return $"Hi, I'm {this.name} and I'm {this.age} years old.";
    }
}

// Creating an object
Person person = new Person("John", 30);
Console.WriteLine(person.Introduce());
```

### Key Differences

| Aspect | PHP | C# |
|--------|-----|-----|
| **File Structure** | Multiple classes per file OK | One public class per file (convention) |
| **Constructor Name** | `__construct()` | Same as class name |
| **Variable Prefix** | `$` required | No prefix |
| **Member Access** | `$this->` | `this.` |
| **Method Naming** | camelCase or snake_case | PascalCase (convention) |
| **Everything is a class** | No | Yes (even `Program` has a class) |

---

## Properties vs Fields

This is one of the biggest differences between PHP and C#.

### PHP - Public Variables
```php
<?php
class Product 
{
    // Public field (direct access)
    public $name;
    public $price;
    
    // Using getter/setter methods for validation
    private $discount = 0;
    
    public function setDiscount($value) 
    {
        if ($value >= 0 && $value <= 100) {
            $this->discount = $value;
        }
    }
    
    public function getDiscount() 
    {
        return $this->discount;
    }
}

$product = new Product();
$product->name = "Laptop";        // Direct access
$product->setDiscount(10);        // Through method
```

### C# - Properties (Recommended)
```csharp
public class Product
{
    // Auto-implemented properties (most common)
    public string Name { get; set; }
    public decimal Price { get; set; }
    
    // Property with backing field and validation
    private int discount;
    public int Discount
    {
        get { return discount; }
        set 
        {
            if (value >= 0 && value <= 100)
                discount = value;
            else
                throw new ArgumentException("Discount must be between 0 and 100");
        }
    }
    
    // Read-only property
    public decimal DiscountedPrice
    {
        get { return Price * (1 - Discount / 100m); }
    }
    
    // Expression-bodied property (C# 6+)
    public string DisplayName => $"{Name} - ${Price}";
}

// Usage
Product product = new Product();
product.Name = "Laptop";          // Looks like field, actually property
product.Price = 999.99m;
product.Discount = 10;
Console.WriteLine(product.DiscountedPrice);  // 899.991
```

### Property Variations in C#

```csharp
public class Employee
{
    // Auto-property with default value
    public string Name { get; set; } = "Unknown";
    
    // Auto-property with private setter (read-only from outside)
    public int Id { get; private set; }
    
    // Init-only property (C# 9+, can only set during initialization)
    public DateTime HireDate { get; init; }
    
    // Computed property
    public int YearsOfService => DateTime.Now.Year - HireDate.Year;
    
    // Property with different access levels
    public decimal Salary { get; private set; }
    
    public Employee(int id)
    {
        Id = id;  // Can set in constructor
    }
    
    public void IncreaseSalary(decimal amount)
    {
        Salary += amount;  // Can modify internally
    }
}

// Usage
var emp = new Employee(101) 
{ 
    Name = "Alice",
    HireDate = new DateTime(2020, 1, 15)  // init property
};

Console.WriteLine(emp.YearsOfService);  // Computed
// emp.Id = 102;  // Error! Private setter
// emp.HireDate = DateTime.Now;  // Error! Init-only
```

### Why Properties Over Public Fields?

**C# Best Practice**: Always use properties, not public fields.

```csharp
// ❌ Don't do this (PHP style)
public class BadExample
{
    public string Name;  // Public field
}

// ✅ Do this (C# style)
public class GoodExample
{
    public string Name { get; set; }  // Property
}
```

**Reasons:**
1. Can add validation later without breaking code
2. Can add logging/debugging
3. Can make read-only or write-only
4. Works better with frameworks (serialization, data binding)
5. Can override in derived classes

---

## Methods

### PHP Methods
```php
<?php
class Calculator 
{
    // Instance method
    public function add($a, $b) 
    {
        return $a + $b;
    }
    
    // Method with type hints (PHP 7+)
    public function multiply(int $a, int $b): int 
    {
        return $a * $b;
    }
    
    // Method with default parameters
    public function power($base, $exponent = 2) 
    {
        return pow($base, $exponent);
    }
}
```

### C# Methods
```csharp
public class Calculator
{
    // Instance method
    public int Add(int a, int b)
    {
        return a + b;
    }
    
    // Expression-bodied method (concise syntax)
    public int Multiply(int a, int b) => a * b;
    
    // Method with default parameters
    public double Power(double baseNum, double exponent = 2)
    {
        return Math.Pow(baseNum, exponent);
    }
    
    // Method overloading (same name, different signatures)
    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }
    
    public double Add(double a, double b)
    {
        return a + b;
    }
    
    // Out parameters (multiple return values)
    public bool TryDivide(int a, int b, out double result)
    {
        if (b == 0)
        {
            result = 0;
            return false;
        }
        result = (double)a / b;
        return true;
    }
    
    // Ref parameters (pass by reference)
    public void Increment(ref int number)
    {
        number++;
    }
}

// Usage
var calc = new Calculator();
Console.WriteLine(calc.Add(5, 3));           // 8
Console.WriteLine(calc.Add(5, 3, 2));        // 10 (overloaded version)
Console.WriteLine(calc.Power(5));            // 25 (using default parameter)

// Out parameter
if (calc.TryDivide(10, 2, out double result))
{
    Console.WriteLine($"Result: {result}");  // Result: 5
}

// Ref parameter
int num = 5;
calc.Increment(ref num);
Console.WriteLine(num);  // 6
```

### Method Naming Conventions

| PHP | C# |
|-----|-----|
| `getUserName()` | `GetUserName()` |
| `calculate_total()` | `CalculateTotal()` |
| `is_valid()` | `IsValid()` |

**C# Convention**: PascalCase for all public methods

---

## Constructors

### PHP Constructors
```php
<?php
class User 
{
    private $id;
    private $name;
    private $email;
    
    // Single constructor
    public function __construct($id, $name, $email = null) 
    {
        $this->id = $id;
        $this->name = $name;
        $this->email = $email ?? "noemail@example.com";
    }
}

$user1 = new User(1, "John");
$user2 = new User(2, "Jane", "jane@example.com");
```

### C# Constructors
```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
    
    // Default constructor (parameterless)
    public User()
    {
        Email = "noemail@example.com";
    }
    
    // Constructor with parameters
    public User(int id, string name)
    {
        Id = id;
        Name = name;
        Email = "noemail@example.com";
    }
    
    // Constructor overloading
    public User(int id, string name, string email)
    {
        Id = id;
        Name = name;
        Email = email;
    }
    
    // Constructor chaining (calling another constructor)
    public User(int id, string name, string email, DateTime createdDate) 
        : this(id, name, email)  // Calls the 3-parameter constructor first
    {
        CreatedDate = createdDate;
    }
    
    public DateTime CreatedDate { get; set; } = DateTime.Now;
}

// Usage
var user1 = new User();  // Default constructor
var user2 = new User(1, "John");  // 2-parameter
var user3 = new User(2, "Jane", "jane@example.com");  // 3-parameter
```

### Modern C# - Primary Constructors (C# 12+)
```csharp
// Concise syntax
public class User(int id, string name, string email)
{
    public int Id { get; } = id;
    public string Name { get; } = name;
    public string Email { get; } = email;
    
    public void PrintInfo()
    {
        Console.WriteLine($"{id}: {name} ({email})");
    }
}
```

---

## Access Modifiers

### Comparison Table

| Access Modifier | PHP | C# | Meaning |
|----------------|-----|-----|---------|
| **Public** | `public` | `public` | Accessible from anywhere |
| **Private** | `private` | `private` | Only within the same class |
| **Protected** | `protected` | `protected` | Class and derived classes |
| **Internal** | N/A | `internal` | Within the same assembly/project |
| **Protected Internal** | N/A | `protected internal` | Protected OR Internal |
| **Private Protected** | N/A | `private protected` | Protected AND Internal |

### PHP Example
```php
<?php
class BankAccount 
{
    private $balance = 0;           // Only this class
    protected $accountNumber;       // This class + derived classes
    public $accountHolder;          // Accessible everywhere
    
    public function deposit($amount) 
    {
        $this->balance += $amount;  // OK, same class
    }
    
    private function calculateInterest() 
    {
        return $this->balance * 0.05;
    }
}
```

### C# Example
```csharp
public class BankAccount
{
    private decimal balance = 0;              // Only this class
    protected string accountNumber;           // This class + derived classes
    public string AccountHolder { get; set; } // Accessible everywhere
    internal string BankCode { get; set; }    // Same assembly only
    
    public void Deposit(decimal amount)
    {
        balance += amount;  // OK, same class
        LogTransaction();   // OK, private method
    }
    
    private void LogTransaction()
    {
        // Private helper method
    }
    
    protected decimal CalculateInterest()
    {
        return balance * 0.05m;
    }
}
```

### Default Access Modifiers

```csharp
// If you don't specify, C# uses these defaults:
class MyClass              // internal (not public!)
{
    int field;             // private
    void Method() { }      // private
}

// Always be explicit for clarity!
public class MyClass       // ✅ Better
{
    private int field;     // ✅ Clear
    public void Method() { } // ✅ Clear
}
```

---

## Namespaces

Namespaces organize code and prevent naming conflicts.

### PHP Namespaces
```php
<?php
// File: src/Models/User.php
namespace MyApp\Models;

class User 
{
    public $name;
}

// File: src/Services/UserService.php
namespace MyApp\Services;

use MyApp\Models\User;  // Import

class UserService 
{
    public function createUser($name) 
    {
        return new User();  // Can use short name
    }
}
```

### C# Namespaces
```csharp
// File: Models/User.cs
namespace MyApp.Models
{
    public class User
    {
        public string Name { get; set; }
    }
}

// File: Services/UserService.cs
using MyApp.Models;  // Import namespace

namespace MyApp.Services
{
    public class UserService
    {
        public User CreateUser(string name)
        {
            return new User { Name = name };
        }
    }
}

// Modern C# - File-scoped namespace (C# 10+)
namespace MyApp.Services;  // No braces, applies to whole file

public class UserService
{
    public User CreateUser(string name)
    {
        return new User { Name = name };
    }
}
```

### Using Aliases
```csharp
using Project = MyApp.Models.Project;
using Task = MyApp.Models.Task;  // Not System.Threading.Tasks.Task

namespace MyApp
{
    public class Example
    {
        public void Test()
        {
            var project = new Project();  // MyApp.Models.Project
            var task = new Task();        // MyApp.Models.Task
        }
    }
}
```

---

## Static Members

Static members belong to the class itself, not instances.

### PHP Static Members
```php
<?php
class Database 
{
    private static $instance = null;
    private static $connectionCount = 0;
    
    public static function getInstance() 
    {
        if (self::$instance === null) {
            self::$instance = new Database();
        }
        return self::$instance;
    }
    
    public static function getConnectionCount() 
    {
        return self::$connectionCount;
    }
}

db = Database::getInstance();
echo Database::getConnectionCount();
```

### C# Static Members
```csharp
public class MathHelper
{
    // Static field
    public static readonly double Pi = 3.14159;
    
    // Static property
    public static int CalculationCount { get; private set; }
    
    // Static method
    public static double CircleArea(double radius)
    {
        CalculationCount++;
        return Pi * radius * radius;
    }
    
    // Static constructor (runs once when class is first used)
    static MathHelper()
    {
        Console.WriteLine("MathHelper initialized");
    }
}

// Usage - no instance needed
double area = MathHelper.CircleArea(5);
Console.WriteLine($"Calculations performed: {MathHelper.CalculationCount}");
Console.WriteLine($"Pi value: {MathHelper.Pi}");
```

### Static Class (C# only)
```csharp
// Static class - cannot be instantiated, only static members
public static class Configuration
{
    public static string ConnectionString { get; set; }
    public static bool IsProduction { get; set; }
    
    public static void Load()
    {
        // Load configuration
    }
}

// Usage
Configuration.Load();
Configuration.ConnectionString = "Server=localhost";
// var config = new Configuration();  // Error! Can't instantiate static class
```

---

## The `this` Keyword

### PHP `$this`
```php
<?php
class Person 
{
    private $name;
    
    public function __construct($name) 
    {
        $this->name = $name;  // Must use $this->
    }
    
    public function greet() 
    {
        return "Hello, I'm " . $this->name;
    }
}
```

### C# `this`
```csharp
public class Person
{
    private string name;
    
    public Person(string name)
    {
        this.name = name;  // Distinguish parameter from field
    }
    
    // Can omit 'this.' if no ambiguity
    public string Greet()
    {
        return $"Hello, I'm {name}";  // 'this.' is optional here
    }
    
    // Passing current instance to another method
    public void Register()
    {
        UserManager.RegisterUser(this);  // Pass current object
    }
}
```

### Extension Methods (C# Feature)
```csharp
// Extension methods allow adding methods to existing types
public static class StringExtensions
{
    // 'this' in first parameter makes it an extension method
    public static bool IsValidEmail(this string email)
    {
        return email.Contains("@");
    }
}

// Usage - looks like instance method!
string email = "test@example.com";
bool valid = email.IsValidEmail();  // Called as if it's a string method
```

---

## Object Initialization

### PHP Object Creation
```php
<?php
class Product 
{
    public $name;
    public $price;
    public $category;
}

// Traditional
$product = new Product();
$product->name = "Laptop";
$product->price = 999.99;
$product->category = "Electronics";
```

### C# Object Initializers
```csharp
public class Product
{
    public string Name { get; set; }
    public decimal Price { get; set; }
    public string Category { get; set; }
}

// Object initializer syntax
Product product = new Product
{
    Name = "Laptop",
    Price = 999.99m,
    Category = "Electronics"
};

// Or with target-typed new (C# 9+)
Product product = new()
{
    Name = "Laptop",
    Price = 999.99m,
    Category = "Electronics"
};

// Collection initializer
List<Product> products = new()
{
    new() { Name = "Laptop", Price = 999.99m },
    new() { Name = "Mouse", Price = 25.99m },
    new() { Name = "Keyboard", Price = 75.00m }
};
```

### Anonymous Types (C# Only)
```csharp
// Create object without defining a class
var person = new
{
    Name = "John",
    Age = 30,
    City = "New York"
};

Console.WriteLine($"{person.Name} is {person.Age}");
// person.Name = "Jane";  // Error! Anonymous types are immutable
```

---

## Reference Links

- [C# Classes and Objects](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/types/classes)
- [Properties in C#](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/properties)
- [Methods in C#](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods)
- [Access Modifiers](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers)
- [Namespaces](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/types/namespaces)
- [Static Classes and Members](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members)

---

## Exercises

### Exercise 1: Book Class
Create a `Book` class with the following requirements:

**PHP Version (for reference):**
```php
<?php
class Book 
{
    private $title;
    private $author;
    private $isbn;
    private $price;
    
    public function __construct($title, $author, $isbn, $price) 
    {
        $this->title = $title;
        $this->author = $author;
        $this->isbn = $isbn;
        $this->price = $price;
    }
    
    public function getDescription() 
    {
        return "{$this->title}" by {$this->author};
    }
    
    public function applyDiscount($percentage) 
    {
        $this->price -= $this->price * ($percentage / 100);
    }
}
```

**Your C# Task:**
1. Convert the above to C# using properties
2. Add a read-only `PublicationYear` property
3. Add a computed property `IsExpensive` (true if price > 50)
4. Use object initializer syntax to create instances

### Exercise 2: BankAccount Class
Create a `BankAccount` class:

**Requirements:**
- Private field for `balance`
- Public properties: `AccountNumber` (read-only), `AccountHolder`
- Methods: `Deposit(amount)`, `Withdraw(amount)`, `GetBalance()`
- Validation: Don't allow negative deposits, don't allow overdrafts
- Static property: `TotalAccounts` (increments with each new account)
- Static method: `GetTotalAccounts()`

**Test your implementation:**
```csharp
var account1 = new BankAccount("12345", "John Doe");
var account2 = new BankAccount("67890", "Jane Smith");

account1.Deposit(1000);
account1.Withdraw(200);

Console.WriteLine($"Balance: ${account1.GetBalance()}");
Console.WriteLine($"Total accounts: {BankAccount.GetTotalAccounts()}");
```

### Exercise 3: Product Catalog
Create classes for a product catalog:

**Requirements:**
1. `Product` class with:
   - Properties: `Id`, `Name`, `Price`, `Stock`
   - Method: `IsInStock()` returns bool
   - Static property: `NextId` (auto-incrementing)

2. `ProductCatalog` class with:
   - List of products
   - Methods: `AddProduct()`, `FindById()`, `GetExpensiveProducts(decimal threshold)`

**Test with object initializers:**
```csharp
var catalog = new ProductCatalog();

catalog.AddProduct(new Product 
{ 
    Name = "Laptop", 
    Price = 999.99m, 
    Stock = 5 
});

var expensive = catalog.GetExpensiveProducts(500);
```

### Exercise 4: Temperature Converter
Create a `Temperature` class with:

**Requirements:**
- Private field for celsius value
- Property `Celsius` with getter and setter
- Read-only properties `Fahrenheit` and `Kelvin` (computed from Celsius)
- Constructor accepting celsius value
- Method `ToString()` override showing all three formats

**Formulas:**
- Fahrenheit = (Celsius × 9/5) + 32
- Kelvin = Celsius + 273.15

**Test:**
```csharp
var temp = new Temperature(25);
Console.WriteLine(temp.ToString());
// Output: 25°C = 77°F = 298.15K

temp.Celsius = 0;
Console.WriteLine(temp.Fahrenheit);  // 32
```

### Exercise 5: Namespace Organization
Create a mini project structure:

```
MyStore/
├── Models/
│   ├── Product.cs
│   └── Customer.cs
└── Services/
    └── OrderService.cs
```

**Requirements:**
1. `Product` in `MyStore.Models` namespace
2. `Customer` in `MyStore.Models` namespace  
3. `OrderService` in `MyStore.Services` namespace that uses both Model classes
4. Use proper `using` statements

---

## Solutions

Detailed solutions for all exercises can be found in [/exercises/04-oop-fundamentals/](./exercises/04-oop-fundamentals/)

---

**Previous**: [03 - Type System](./03-type-system.md) | **Next**: [05 - Advanced OOP](./05-advanced-oop.md)