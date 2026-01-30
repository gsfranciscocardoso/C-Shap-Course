# Module 02: Syntax Comparison - PHP vs C#

## Overview

This module provides a side-by-side comparison of PHP and C# syntax for common programming constructs. Understanding these mappings will accelerate your learning.

## Variables and Data Types

### PHP (Loose Typing)
```php
<?php
$name = "John";           // string
$age = 30;                // int
$price = 19.99;           // float
$isActive = true;         // bool
$items = [1, 2, 3];       // array
$person = null;           // null
```

### C# (Strong Typing)
```csharp
string name = "John";           // string
int age = 30;                   // int
double price = 19.99;           // double
bool isActive = true;           // bool
int[] items = {1, 2, 3};        // array
string person = null;           // null (with nullable reference types)

// Type inference with 'var' (still strongly typed)
var name = "John";              // Compiler infers string
var age = 30;                   // Compiler infers int
```

### Key Differences
- C# requires type declaration (or `var` for inference)
- C# types are checked at compile-time
- No `$` prefix for variables in C#
- C# uses `;` for every statement

## Data Types Mapping

| PHP | C# | Notes |
|-----|-----|-------|
| `int` | `int` | 32-bit integer |
| `float` | `float` | 32-bit floating point |
| `float` / `double` | `double` | 64-bit floating point (more common) |
| `string` | `string` | Immutable in C# |
| `bool` | `bool` | `true` / `false` (lowercase in C#) |
| `array` | `array[]` or `List<T>` | Fixed vs dynamic size |
| `null` | `null` | Requires nullable types in C# 8+ |
| `object` | `object` | Base type for all types |

## String Operations

### PHP
```php
<?php
$name = "John";
$greeting = "Hello, $name";           // Interpolation with double quotes
$greeting2 = 'Hello, ' . $name;       // Concatenation
$length = strlen($greeting);
$upper = strtoupper($name);
$substring = substr($name, 0, 2);
```

### C#
```csharp
string name = "John";
string greeting = $"Hello, {name}";              // String interpolation
string greeting2 = "Hello, " + name;             // Concatenation
int length = greeting.Length;                     // Property, not function
string upper = name.ToUpper();                   // Method call
string substring = name.Substring(0, 2);
```

### String Methods Comparison

| PHP | C# | Example |
|-----|-----|---------|
| `strlen($str)` | `str.Length` | "hello".Length → 5 |
| `strtoupper($str)` | `str.ToUpper()` | "hello".ToUpper() → "HELLO" |
| `strtolower($str)` | `str.ToLower()` | "HELLO".ToLower() → "hello" |
| `substr($str, $start, $len)` | `str.Substring(start, len)` | "hello".Substring(0, 2) → "he" |
| `str_replace($search, $replace, $str)` | `str.Replace(search, replace)` | "hello".Replace("l", "L") → "heLLo" |
| `trim($str)` | `str.Trim()` | " hi ".Trim() → "hi" |
| `explode($delimiter, $str)` | `str.Split(delimiter)` | "a,b,c".Split(',') |
| `implode($glue, $array)` | `string.Join(glue, array)` | `string.Join(",", arr)` |

## Arrays and Collections

### PHP Arrays (Dynamic)
```php
<?php
// Indexed array
$numbers = [1, 2, 3, 4, 5];
$numbers[] = 6;                    // Add element
$count = count($numbers);
$first = $numbers[0];

// Associative array
$person = [
    'name' => 'John',
    'age' => 30,
    'city' => 'New York'
];
$name = $person['name'];
```

### C# Arrays (Fixed Size)
```csharp
// Array (fixed size)
int[] numbers = {1, 2, 3, 4, 5};
int count = numbers.Length;
int first = numbers[0];

// Cannot add elements to array after creation
// Use List<T> for dynamic arrays
```

### C# List (Dynamic, like PHP arrays)
```csharp
using System.Collections.Generic;

// List<T> - similar to PHP indexed arrays
List<int> numbers = new List<int> {1, 2, 3, 4, 5};
numbers.Add(6);                    // Add element
int count = numbers.Count;
int first = numbers[0];

// Dictionary<TKey, TValue> - similar to PHP associative arrays
Dictionary<string, object> person = new Dictionary<string, object>
{
    {"name", "John"},
    {"age", 30},
    {"city", "New York"}
};
string name = (string)person["name"];
```

## Control Structures

### If Statements

**PHP:**
```php
<?php
if ($age >= 18) {
    echo "Adult";
} elseif ($age >= 13) {
    echo "Teenager";
} else {
    echo "Child";
}
```

**C#:**
```csharp
if (age >= 18)
{
    Console.WriteLine("Adult");
}
else if (age >= 13)    // Note: 'else if', not 'elseif'
{
    Console.WriteLine("Teenager");
}
else
{
    Console.WriteLine("Child");
}
```

### Switch Statements

**PHP:**
```php
<?php
switch ($day) {
    case 'Monday':
        echo "Start of week";
        break;
    case 'Friday':
        echo "End of week";
        break;
    default:
        echo "Midweek";
}
```

**C#:**
```csharp
switch (day)
{
    case "Monday":
        Console.WriteLine("Start of week");
        break;
    case "Friday":
        Console.WriteLine("End of week");
        break;
    default:
        Console.WriteLine("Midweek");
        break;
}

// Modern C# - Switch expression
string message = day switch
{
    "Monday" => "Start of week",
    "Friday" => "End of week",
    _ => "Midweek"  // _ is like default
};
```

### Loops

**PHP:**
```php
<?php
// For loop
for ($i = 0; $i < 10; $i++) {
    echo $i;
}

// Foreach
foreach ($items as $item) {
    echo $item;
}

foreach ($person as $key => $value) {
    echo "$key: $value";
}

// While
while ($condition) {
    // code
}
```

**C#:**
```csharp
// For loop
for (int i = 0; i < 10; i++)
{
    Console.WriteLine(i);
}

// Foreach
foreach (var item in items)
{
    Console.WriteLine(item);
}

foreach (var kvp in person)
{
    Console.WriteLine($"{kvp.Key}: {kvp.Value}");
}

// While
while (condition)
{
    // code
}
```

## Functions / Methods

### PHP
```php
<?php
function greet($name, $greeting = "Hello") {
    return "$greeting, $name!";
}

$message = greet("John");
$message2 = greet("Jane", "Hi");
```

### C#
```csharp
// Method (must be inside a class)
static string Greet(string name, string greeting = "Hello")
{
    return $"{greeting}, {name}!";
}

string message = Greet("John");
string message2 = Greet("Jane", "Hi");

// Modern C# - Local function
string Greet(string name, string greeting = "Hello")
{
    return $"{greeting}, {name}!";
}
```

### Type Declarations

**PHP 7+:**
```php
<?php
function add(int $a, int $b): int {
    return $a + $b;
}
```

**C#:**
```csharp
int Add(int a, int b)
{
    return a + b;
}

// Expression-bodied method
int Add(int a, int b) => a + b;
```

## Null Handling

### PHP
```php
<?php
$value = null;
$name = $value ?? "Default";           // Null coalescing
$length = $value?.length ?? 0;         // Null safe operator
```

### C#
```csharp
string value = null;
string name = value ?? "Default";            // Null coalescing
int length = value?.Length ?? 0;             // Null conditional

// Nullable value types
int? nullableInt = null;                     // int? means nullable int
int number = nullableInt ?? 0;
```

## Class Basics

### PHP
```php
<?php
class Person {
    private $name;
    private $age;
    
    public function __construct($name, $age) {
        $this->name = $name;
        $this->age = $age;
    }
    
    public function greet() {
        return "Hello, I'm {
            $this->name";
    }
}

$person = new Person("John", 30);
echo $person->greet();
```

### C#
```csharp
class Person
{
    private string name;
    private int age;
    
    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }
    
    public string Greet()
    {
        return $"Hello, I'm {this.name}";
    }
}

Person person = new Person("John", 30);
Console.WriteLine(person.Greet());
```

## Operators

Most operators are the same, but note these differences:

| Operation | PHP | C# |
|-----------|-----|-----|
| String concatenation | `.` | `+` |
| Identical comparison | `===` | N/A (use `==` for value, `ReferenceEquals` for reference) |
| Not identical | `!==` | N/A |
| Logical AND | `&&` or `and` | `&&` |
| Logical OR | `
|` or `or` | `
|` |
| String interpolation | `"Hello, $name"` | `$"Hello, {name}"` |

## Reference Links

- [C# Language Reference](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/)
- [C# Keywords](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/)
- [C# Operators](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/)
- [Built-in Types](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/built-in-types)

## Exercises

### Exercise 1: Variable Practice
Convert this PHP code to C#:
```php
<?php
$firstName = "John";
$lastName = "Doe";
$age = 30;
$salary = 50000.50;
$isEmployed = true;

$fullName = "$firstName $lastName";
echo "Name: $fullName, Age: $age, Employed: " . ($isEmployed ? "Yes" : "No");
```

### Exercise 2: Array Manipulation
Convert this PHP code to C# using `List<T>`:
```php
<?php
$numbers = [1, 2, 3, 4, 5];
$numbers[] = 6;
$numbers[] = 7;

$sum = 0;
foreach ($numbers as $num) {
    $sum += $num;
}

echo "Sum: $sum\n";
echo "Count: " . count($numbers);
```

### Exercise 3: Dictionary Practice
Convert this PHP associative array to C# Dictionary:
```php
<?php
$products = [
    'laptop' => 999.99,
    'mouse' => 25.50,
    'keyboard' => 75.00
];

foreach ($products as $name => $price) {
    echo "$name: $$price\n";
}

$products['monitor'] = 299.99;
```

### Exercise 4: Control Flow
Create a C# program that:
1. Accepts a number from the user
2. Uses a switch expression (modern C#) to output:
   - "One" if 1
   - "Two" if 2
   - "Three" if 3
   - "Other number" for anything else

### Exercise 5: String Manipulation
Write a C# program that:
1. Takes a full name as input
2. Splits it into first and last name
3. Converts first name to uppercase
4. Converts last name to lowercase
5. Outputs: "FIRSTNAME lastname"

## Solutions

Solutions can be found in [/exercises/02-syntax-comparison/](./exercises/02-syntax-comparison/)

---

**Previous**: [01 - Getting Started](./01-getting-started.md) | **Next**: [03 - Type System](./03-type-system.md)