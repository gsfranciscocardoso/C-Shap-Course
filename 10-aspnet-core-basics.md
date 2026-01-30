# ASP.NET Core Basics

## MVC Pattern
The Model-View-Controller pattern separates concerns in web applications.

## Controllers
Controllers handle incoming requests and responses.

### Example:
```csharp
public class HomeController : Controller {
    public IActionResult Index() {
        return View();
    }
}
```

## Views
Views represent the user interface.

## Routing
Routing maps requests to the corresponding controller actions.

## Middleware
Middleware processes requests and responses in a pipeline.

## Exercises
1. Create a basic controller and a view for a simple app.
2. Implement a middleware component that logs requests.