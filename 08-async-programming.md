# Module 08: Asynchronous Programming in C#  

Asynchronous programming is a powerful technique that enables you to write programs that can perform many tasks concurrently without blocking the execution of other tasks. C# offers built-in support for asynchronous programming with async and await keywords, Task-based programming, parallel programming constructs, and features for better error handling.

## Table of Contents  
- [Introduction to Asynchronous Programming](#introduction)  
- [Async/Await in C#](#async-await)  
- [Task and Task<TResult>](#task)  
- [Parallel Programming](#parallel-programming)  
- [Error Handling](#error-handling)  
- [Comparisons with PHP](#php-comparison)  
- [Exercises](#exercises)  

### <a name="introduction"></a>Introduction to Asynchronous Programming  
Asynchronous programming allows you to execute tasks independently while being able to handle other tasks without waiting for them to complete. This model is particularly useful for I/O-bound work like web requests, file operations, etc.

### <a name="async-await"></a>Async/Await in C#  
The `async` keyword enables the `await` operator, which allows for an asynchronous call to be made without blocking the current thread.  
Here's a simple example in C#:
```csharp
public async Task ExampleAsync()  
{
    var result = await SomeAsyncOperation();  
    Console.WriteLine(result);
}
```

### <a name="task"></a>Task and Task<TResult>  
Tasks represent asynchronous operations in C#.  
- `Task`: Represents an asynchronous operation that does not return a value.  
- `Task<TResult>`: Represents an asynchronous operation that returns a value.

Example:
```csharp
public async Task<string> GetDataAsync()  
{
    return await Task.FromResult("data");
}
```

### <a name="parallel-programming"></a>Parallel Programming  
C# provides the `Parallel` class to simplify parallel operations execution. Here's an example:
```csharp
Parallel.For(0, 10, (i) =>  
{
    Console.WriteLine("Task {0} is running.", i);
});
```

### <a name="error-handling"></a>Error Handling  
Error handling in asynchronous methods can be done using try/catch blocks. Example:
```csharp
try  
{
    await ExampleAsync();
}  
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

### <a name="php-comparison"></a>Comparisons with PHP  
| Feature       | C#                       | PHP                               |
|---------------|--------------------------|-----------------------------------|
| Async Model   | Async/Await              | Promises (e.g., Guzzle)           |
| Syntax        | `async`/`await`         | `Promise` with `then()`           |
| Parallel      | `Parallel.For`          | `parallel` extension               |
| Error Handling | Try/Catch              | Exception handling                 |

### <a name="exercises"></a>Exercises  
1. Implement a simple API call using async/await in C#.  
2. Create a comparison of synchronous vs asynchronous code performance in C#.  
3. Write a parallel processing example.

### References  
- [Microsoft Docs - Asynchronous Programming](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/async/)  
- [PHP: Asynchronous Programming](https://www.php.net/manual/en/book.promise.php)  

---  

### Navigation  
- [Previous Module: 07 - Database Access](07-database-access.md)  
- [Next Module: 09 - Web Development](09-web-development.md)  

---