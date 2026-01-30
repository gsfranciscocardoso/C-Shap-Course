# Asynchronous Programming in C#

## async/await
Using `async` and `await` keywords for non-blocking code.

### Example:
```csharp
public async Task FetchDataAsync() {
    var data = await GetDataFromApi();
}
```

## Task
Represents an asynchronous operation.

## Asynchronous Patterns
Common patterns include callbacks and promises.

## Exercises
1. Create an async method to download a file.
2. Implement error handling in async methods.