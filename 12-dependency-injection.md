# Dependency Injection in C#

## DI Container
ASP.NET Core has a built-in dependency injection container.

## Service Lifetimes
Understand service lifetimes: Transient, Scoped, Singleton.

## Constructor Injection
Inject dependencies through constructors.

### Example:
```csharp
public class CarService {
    private readonly IDatabase db;
    public CarService(IDatabase db) {
        this.db = db;
    }
}
```

## Exercises
1. Implement a service that uses constructor injection.
2. Create a simple interface and a class that implements it, then inject it into a controller.