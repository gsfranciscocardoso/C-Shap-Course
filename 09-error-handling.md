# Error Handling in C#

## Exceptions
Exceptions are runtime errors that can be handled gracefully.

### Example:
```csharp
try {
    int result = 10 / 0;
} catch (DivideByZeroException ex) {
    Console.WriteLine(ex.Message);
}
```

## try-catch-finally
A structured way to manage exceptions.

## Custom Exceptions
Define your own exception types.

### Example:
```csharp
public class MyCustomException : Exception {
    public MyCustomException(string message): base(message) {}
}
```

## Exercises
1. Create a custom exception for invalid input.
2. Implement a try-catch block in your methods to handle exceptions gracefully.