# Module 03: Type System - Understanding Strong Typing

## Overview

One of the biggest differences between PHP and C# is the type system. C# is strongly and statically typed, meaning type errors are caught at compile-time rather than runtime.

## PHP Type Evolution

PHP has evolved from loosely typed to optionally typed:

```php
<?php
// PHP 5 - No type hints
function add($a, $b) {
    return $a + $b;
}

// PHP 7+ - Optional type hints
function add(int $a, int $b): int {
    return $a + $b;
}

// Still allows this
$result = add("5", "10");  // Works, strings coerced to ints
```

## C# Strong Typing

C# requires explicit types and performs compile-time type checking:

```csharp
int Add(int a, int b)
{
    return a + b;
}

int result = Add(5, 10);        // OK
// int result = Add("5", "10"); // Compile error!
```

## Value Types vs Reference Types

### Value Types
Stored on the stack, contain the actual data:

```csharp
// Value types
int number = 42;
double price = 19.99;
bool isActive = true;
char letter = 'A';

struct Point
{
    public int X;
    public int Y;
}

Point p1 = new Point { X = 10, Y = 20 };
Point p2 = p1;      // Copies the value
p2.X = 30;          // p1.X is still 10
```

### Reference Types
Stored on the heap, variables hold references:

```csharp
// Reference types
string name = "John";
object obj = new object();
int[] numbers = {1, 2, 3};

class Person
{
    public string Name { get; set; }
}

Person p1 = new Person { Name = "John" };
Person p2 = p1;          // Copies the reference
p2.Name = "Jane";        // p1.Name is now also "Jane"
```

**PHP Comparison:**
```php
<?php
// PHP objects are references
class Person {
    public $name;
}

$p1 = new Person();
$p1->name = "John";
$p2 = $p1;              // Reference
$p2->name = "Jane";     // $p1->name is now "Jane"

// PHP primitives and arrays are values (copy-on-write)
$a = [1, 2, 3];
$b = $a;                // Copy
$b[] = 4;               // $a is still [1, 2, 3]
```

## Built-in Types

### Numeric Types

| C# Type | Size | Range | PHP Equivalent |
|---------|------|-------|----------------|
| `byte` | 8-bit | 0 to 255 | - |
| `short` | 16-bit | -32,768 to 32,767 | - |
| `int` | 32-bit | -2.1B to 2.1B | `int` |
| `long` | 64-bit | -9.2E18 to 9.2E18 | - |
| `float` | 32-bit | ±1.5E-45 to ±3.4E38 | `float` |
| `double` | 64-bit | ±5.0E-324 to ±1.7E308 | `float` |
| `decimal` | 128-bit | High precision | - |

```csharp
int integer = 42;
long bigNumber = 1000000000L;       // L suffix for long
float smallDecimal = 3.14f;         // f suffix for float
double largeDecimal = 3.14159;      // default for decimals
decimal money = 19.99m;             // m suffix for decimal (use for currency!)
```

**When to use `decimal`**: Always for money/financial calculations!

```csharp
// ❌ Wrong - floating point precision issues
double price = 0.1 + 0.2;  // 0.30000000000000004

// ✅ Correct - decimal is precise
decimal price = 0.1m + 0.2m;  // Exactly 0.3
```

### Boolean Type

```csharp
bool isActive = true;
bool isDeleted = false;

// Note: lowercase true/false in C# (unlike PHP's case-insensitive)
// bool wrong = True;  // Compile error!
```

### Character Type

C# has a dedicated `char` type for single characters:

```csharp
char letter = 'A';           // Single quotes for char
string word = "A";           // Double quotes for string

// char is a 16-bit Unicode character
char emoji = '😀';
```

## String Type

Strings are immutable reference types:

```csharp
string name = "John";
string upper = name.ToUpper();  // Creates new string, doesn't modify original

// String is immutable
// name[0] = 'j';  // Compile error!

// Use StringBuilder for mutable strings
using System.Text;
StringBuilder sb = new StringBuilder();
sb.Append("Hello");
sb.Append(" ");
sb.Append("World");
string result = sb.ToString();  // "Hello World"
```

**PHP Comparison:**
```php
<?php
$name = "John";
$name[0] = 'j';  // Allowed in PHP, creates "john"
```

## Nullable Types

C# 8+ introduced nullable reference types for better null safety.

### Nullable Value Types
```csharp
int regularInt = 42;
// regularInt = null;  // Compile error!

int? nullableInt = null;  // ? makes it nullable
nullableInt = 42;

// Checking for null
if (nullableInt.HasValue)
{
    int value = nullableInt.Value;
}

// Or use null-coalescing
int value = nullableInt ?? 0;  // Use 0 if null
```

### Nullable Reference Types (C# 8+)
```csharp
// Enable in .csproj: <Nullable>enable</Nullable>

string nonNullable = "Hello";
// nonNullable = null;  // Warning!

string? nullable = null;  // OK
nullable = "Hello";

// Must check for null
if (nullable != null)
{
    int length = nullable.Length;  // Safe
}

// Or use null-conditional operator
int? length = nullable?.Length;  // null if nullable is null
```

**PHP Comparison:**
```php
<?php
// PHP allows null anywhere (unless using strict types)
$value = null;
$value = "hello";
$value = 42;

// PHP 7.4+ - Typed properties
class User {
    public string $name;     // Cannot be null (unless explicitly nullable)
    public ?string $email;   // Nullable
}
```

## Type Inference with `var`

```csharp
// Explicit typing
string name = "John";
int age = 30;
List<string> items = new List<string>();

// Type inference with var (still strongly typed!)
var name = "John";              // Compiler infers string
var age = 30;                   // Compiler infers int
var items = new List<string>(); // Compiler infers List<string>();

// var doesn't mean "any type" - it's still compile-time checked
// name = 42;  // Compile error! name is string
```

**Best Practice**: Use `var` when the type is obvious from the right side.

## Type Conversion

### Implicit Conversion (Safe)
```csharp
int intValue = 42;
long longValue = intValue;      // OK - int fits in long
double doubleValue = intValue;  // OK - int fits in double
```

### Explicit Conversion (Cast)
```csharp
double doubleValue = 42.7;
int intValue = (int)doubleValue;  // Explicit cast required, loses precision (42)

// Can lose data or throw exception
long bigNumber = 3000000000L;
// int smaller = (int)bigNumber;  // Overflow!
```

### Parsing Strings
```csharp
// Parse (throws exception if invalid)
int number = int.Parse("123");
// int invalid = int.Parse("abc");  // FormatException!

// TryParse (safer)
if (int.TryParse("123", out int result))
{
    Console.WriteLine($"Parsed: {result}");
}
else
{
    Console.WriteLine("Invalid number");
}
```

**PHP Comparison:**
```php
<?php
$number = (int)"123";       // Cast
$number = intval("123");    // Function

// PHP is more forgiving
$weird = (int)"123abc";     // 123 (ignores trailing chars)
```

### ToString()
```csharp
int number = 42;
string text = number.ToString();

// With formatting
decimal price = 19.99m;
string formatted = price.ToString("C");  // $19.99 (currency format)
```

## Enums

C# has proper enumeration types:

```csharp
enum DayOfWeek
{
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday,
    Sunday
}

DayOfWeek today = DayOfWeek.Monday;

// Enum with explicit values
enum HttpStatusCode
{
    OK = 200,
    NotFound = 404,
    ServerError = 500
}

HttpStatusCode status = HttpStatusCode.NotFound;
int statusCode = (int)status;  // 404
```

**PHP Comparison (PHP 8.1+):**
```php
<?php
enum DayOfWeek {
    case Monday;
    case Tuesday;
    case Wednesday;
}

$today = DayOfWeek::Monday;
```

## Tuples

For returning multiple values:

```csharp
// Return multiple values
(string, int) GetPerson()
{
    return ("John", 30);
}

var person = GetPerson();
Console.WriteLine($"{person.Item1} is {person.Item2}");

// Named tuple elements
(string Name, int Age) GetNamedPerson()
{
    return (Name: "John", Age: 30);
}

var (name, age) = GetNamedPerson();  // Deconstruction
Console.WriteLine($"{name} is {age}");
```

**PHP Comparison:**
```php
<?php
function getPerson(): array {
    return ["John", 30];
}

[$name, $age] = getPerson();  // Array destructuring
```

## Type Checking

```csharp
object obj = "Hello";

// is operator
if (obj is string)
{
    string str = (string)obj;
    Console.WriteLine(str.Length);
}

// Pattern matching with is
if (obj is string str)
{
    Console.WriteLine(str.Length);  // str already casted
}

// typeof for type comparison
Type type = typeof(string);
if (obj.GetType() == typeof(string))
{
    Console.WriteLine("It's a string");
}
```

**PHP Comparison:**
```php
<?php
$obj = "Hello";

if (is_string($obj)) {
    echo strlen($obj);
}

if ($obj instanceof MyClass) {
    // ...
}
```

## Reference Links

- [C# Type System](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/types/)
- [Value Types](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-types)
- [Reference Types](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/reference-types)
- [Nullable Types](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/nullable-value-types)
- [Type Conversion](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/types/casting-and-type-conversions)

## Exercises

### Exercise 1: Type Declarations
Create a C# program that declares variables of different types and prints their values and types:
- An integer
- A double
- A decimal (for money)
- A boolean
- A char
- A string
- A nullable int

### Exercise 2: Type Conversion
Write a program that:
1. Takes a string input from the user
2. Tries to parse it as an integer using `TryParse`
3. If successful, multiply by 2 and display
4. If unsuccessful, display an error message

### Exercise 3: Enums
Create an enum for `TrafficLight` with values `Red`, `Yellow`, `Green`. Write a program that:
1. Takes the current light as input
2. Uses a switch expression to output the action (Stop, Slow Down, Go)

### Exercise 4: Value vs Reference
Create a `struct Point` and a `class Person`. Demonstrate the difference:
```csharp
// TODO: Create struct Point with X, Y
// TODO: Create class Person with Name
// TODO: Create two Points, assign one to the other, modify the second
// TODO: Create two Persons, assign one to the other, modify the second
// TODO: Show how Point values are independent, but Person references point to same object
```

### Exercise 5: Nullable Practice
Write a method that accepts a nullable int and returns:
- The value squared if not null
- 0 if null

Test with both null and non-null values.

## Solutions

Solutions can be found in [/exercises/03-type-system/](./exercises/03-type-system/)

---

**Previous**: [02 - Syntax Comparison](./02-syntax-comparison.md) | **Next**: [04 - OOP Fundamentals](./04-oop-fundamentals.md)