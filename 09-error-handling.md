# Error Handling in C#  

## Introduction to Exceptions  
In programming, exceptions are events that disrupt the normal flow of execution. In C#, exceptions are represented as objects, and they inherit from the `System.Exception` class.  

### Common Types of Exceptions  
- **NullReferenceException**: This exception occurs when you try to dereference a null object.  
- **DivideByZeroException**: This occurs when there is an attempt to divide by zero, which is undefined in mathematics.  

## Try-Catch-Finally Blocks  
C# provides a structured way to handle exceptions using `try`, `catch`, and `finally` blocks.  
Here's an example:
```csharp
try {
    int result = 10 / 0;  // This will throw an exception
} catch (DivideByZeroException ex) {
    Console.WriteLine("Cannot divide by zero!" + ex.Message);
} finally {
    Console.WriteLine("Execution completed.");
}
```  

## Throwing Exceptions Manually  
You can also throw exceptions manually using the `throw` keyword. For example:
```csharp
if (someCondition) {
    throw new InvalidOperationException("Invalid operation!"
}
```

## Custom Exceptions  
C# allows creating custom exceptions by inheriting from the `Exception` class:
```csharp
public class MyCustomException : Exception {
    public MyCustomException(string message) : base(message) {}
}
```

## Best Practices for Exception Handling  
- Use specific exceptions rather than general ones.
- Avoid using exceptions for control flow.
- Log exceptions.  

## Comparisons with PHP Exception Handling  
In PHP, exceptions are handled using try-catch blocks as well. Here’s a PHP example:
```php
try {
    $result = 10 / 0; // This will throw an exception
} catch (Exception $e) {
    echo 'Caught exception: ',  $e->getMessage(), "\n";
}
```
In both languages, the concept of catching exceptions is similar, but PHP lacks some structure that C# provides.

## Exception Properties  
Exceptions in C# come with useful properties such as `Message`, `StackTrace`, and more, which can be used for debugging.

## Exercises  
1. Create a method that throws a `NullReferenceException` and handle it.  
2. Implement a custom exception and raise it in the appropriate situation.  
3. Write code to handle `(DivideByZeroException)` errors in various mathematical operations.
4. Compare C# exception handling with another language of your choice.
5. Implement a logging mechanism to capture exceptions in your application.

[Microsoft Documentation](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/exceptions/)  

[Previous Module: 08-async-programming](08-async-programming.md)  
[Next Module: 10-aspnet-core-basics](10-aspnet-core-basics.md)  
