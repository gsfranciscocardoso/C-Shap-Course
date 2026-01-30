# Collections and LINQ in C#

## Arrays
Arrays are fixed-size collections.

### Example:
```csharp
int[] numbers = new int[5];
```

## List
`List<T>` is a dynamic collection.

### Example:
```csharp
List<string> names = new List<string>();
```

## Dictionary
A collection of key/value pairs.

### Example:
```csharp
Dictionary<string, int> ageMap = new Dictionary<string, int>();
```

## LINQ Queries
LINQ queries simplify data access.

### Example:
```csharp
var result = from n in numbers where n > 10 select n;
```

## Lambda Expressions
Lambda expressions provide a concise way to represent anonymous functions.

## Exercises
1. Use LINQ to filter a list of integers.
2. Implement a method using lambda to sort a list of strings.