# Dependency Injection in C#  

## Introduction to Dependency Injection  
Dependency Injection (DI) is a design pattern that allows the removal of hard-coded dependencies and makes it possible to manage them externally. It leads to more modular, testable, and maintainable code.

## DI Container in ASP.NET Core  
ASP.NET Core has a built-in Dependency Injection container. It allows you to register services and manage their lifetimes automatically. The container works by resolving dependencies when a component is requested.

## Service Lifetimes  
In ASP.NET Core, there are three service lifetimes:  
- **Transient**: A new instance is created each time it is requested.  
- **Scoped**: A new instance is created once per request.  
- **Singleton**: A single instance is created and shared throughout the application.  

### Comparison Table  
| Lifetime   | Instance Creation              | Use Case  |  
|------------|---------------------------------|-----------|  
| Transient  | Created with each request       | Lightweight stateless services  |  
| Scoped     | Created once per request        | Services that depend on the request's lifetime  |  
| Singleton  | Created once and reused         | Heavy services that can be shared  |  

## Constructor Injection Examples  
Here’s an example of using constructor injection in an ASP.NET Core controller:
```csharp
public class HomeController : Controller  
{  
    private readonly IProductService _productService;  

    public HomeController(IProductService productService)  
    {  
        _productService = productService;  
    }  
}  
```

## Interface-based Development  
In a payment processor example, you can define an interface and multiple implementations:
```csharp
public interface IPaymentProcessor  
{  
    void ProcessPayment(decimal amount);  
}  

public class PayPalProcessor : IPaymentProcessor  
{  
    public void ProcessPayment(decimal amount)  
    {  
        // PayPal payment processing logic  
    }  
}  

public class StripeProcessor : IPaymentProcessor  
{  
    public void ProcessPayment(decimal amount)  
    {  
        // Stripe payment processing logic  
    }  
}  
```

## PHP Laravel Comparison  
Just like ASP.NET Core, Laravel has a service container for dependency management. Here’s how you can bind interfaces to implementations:
```php
$this->app->bind(IPaymentProcessor::class, PayPalProcessor::class);
```

## Benefits of DI  
- Improves code maintainability.  
- Enhances testability via mocking and stubbing.  
- Increases application flexibility.  

## Testing with DI using Moq  
You can easily test your components by passing mock implementations:
```csharp
var mockPaymentProcessor = new Mock<IPaymentProcessor>();  
mockPaymentProcessor.Setup(m => m.ProcessPayment(It.IsAny<decimal>()));  
```

## Exercises  
1. Implement a service using Transient lifetime.  
2. Make a service Scoped and observe its lifetime through a web request.  
3. Create a Singleton service and use it across multiple controllers.  
4. Use Moq to test a controller's behavior with a mocked service.  
5. Compare DI in ASP.NET Core and PHP Laravel through a simple application.

## Reference Links  
- [Microsoft Documentation on Dependency Injection](https://docs.microsoft.com/en-us/dotnet/core/extensions/dependency-injection)

## Navigation  
- [Previous Module: 11-rest-apis.md](11-rest-apis.md)  
- [Next Module: 13-unit-testing.md](13-unit-testing.md)  
