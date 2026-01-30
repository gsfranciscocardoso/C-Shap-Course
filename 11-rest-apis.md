# Building REST APIs in ASP.NET Core

## Web API
ASP.NET Core provides powerful tools to create web APIs.

### Example:
```csharp
[ApiController]
[Route("api/[controller]")]
public class CarsController : ControllerBase {
    [HttpGet]
    public IActionResult GetCars() {
        return Ok(cars);
    }
}
```

## Routing
Define routes for your API endpoints.

## HTTP Methods
Understand different HTTP methods (GET, POST, PUT, DELETE).

## JSON Serialization
ASP.NET Core handles JSON serialization out of the box.

## Exercises
1. Create an API endpoint to return a list of cars.
2. Implement error handling for your API responses.