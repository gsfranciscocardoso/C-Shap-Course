# Module 06: Collections and LINQ

## Overview
In this module, we will dive into the essential data structures provided by C# and how they facilitate data manipulation. We'll compare C# collections with PHP arrays and explore LINQ, a powerful querying language that enhances the capability of manipulating collections.

## Arrays
### Fixed-Size vs Dynamic
C# arrays are fixed-size, in contrast to dynamic arrays in PHP. Here’s how they work:

```csharp
int[] fixedArray = new int[5]; // Fixed size 5
fixedArray[0] = 1;
```

In PHP, a dynamic array can grow or shrink:

```php
$array = [];
$array[] = 1; // Adds value to array
```

## List<T> 
### PHP Array Equivalent
C# List<T> provides a dynamic array-like structure. Common methods include:
- `Add(T item)`
- `RemoveAt(int index)`
- `Count`
Usage:

```csharp
List<int> myList = new List<int>();
myList.Add(1);
```

## Dictionary<TKey,TValue>
### Associative Arrays
Dictionaries in C# allow key/value pair storage:

```csharp
dictionary<string, int> myDictionary = new Dictionary<string, int>();
myDictionary.Add("key1", 1);
```

## Other Collections
- **HashSet**: A collection of unique elements.
- **Queue**: First-In-First-Out (FIFO) structure.
- **Stack**: Last-In-First-Out (LIFO) structure.

## LINQ Introduction
LINQ (Language Integrated Query) allows for concise data querying.
Comparison to PHP array functions:
- LINQ: `.Where()`, `.Select()`
- PHP: `array_filter()`, `array_map()`

### Method Syntax
Examples:
- `Where`: Filters a sequence based on predicate
- `Select`: Projects each element into a new form

### Query Syntax
Similar to SQL, for example:
```csharp
var query = from item in myList where item > 0 select item;
```

### Working with Complex Objects
LINQ shines when working with complex data structures.

### Lambda Expressions vs PHP Arrow Functions
Lambda syntax in C#:
```csharp
myList.Where(x => x > 0);
```
In PHP:
```php
array_filter($array, fn($x) => $x > 0);
```

## Deferred Execution
LINQ uses deferred execution, meaning queries are not run until results are iterated over.

## Comparison Tables
| Feature          | C#                | PHP              |
|------------------|------------------|-------------------|
| Arrays           | Fixed size       | Dynamic         |
| List<T>         | Dynamic          | Array           |
| Dictionary       | Key/Value pairs  | Associative array|

## Exercises
1. Create a List<T> and perform different operations.
2. Implement a Dictionary<TKey,TValue> and retrieve values.
3. Use LINQ to filter and sort data in a collection.
4. Compare lambda expressions in C# and PHP.
5. Explore the benefits of deferred execution in LINQ.

## Reference Links
- [Microsoft Docs - Collections](https://docs.microsoft.com/en-us/dotnet/standard/collections/)
- [LINQ documentation](https://docs.microsoft.com/en-us/dotnet/csharp/programming/language-reference/keywords/linq)

## Navigation
- [Previous Module: 05-advanced-oop.md](05-advanced-oop.md)
- [Next Module: 07-async-programming.md](07-async-programming.md)