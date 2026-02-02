# Building REST APIs in ASP.NET Core with Comparisons to PHP Laravel

## Overview
In this document, we will explore building REST APIs using ASP.NET Core, and compare it with PHP Laravel across several aspects. We'll cover the following topics:

- API Controllers and CRUD Operations
- HTTP Methods (GET, POST, PUT, DELETE)
- Attribute Routing
- Model Validation with Data Annotations
- HTTP Status Codes
- JSON Serialization
- Error Handling
- Testing with cURL
- Exercises
- Reference Links

## API Controllers and CRUD Operations
- In ASP.NET Core, API controllers are defined by deriving from `ControllerBase`. For instance:
  ```csharp
  [ApiController]
  [Route("api/[controller]")]
  public class ProductsController : ControllerBase
  {
      // GET: api/products
      [HttpGet]
      public IEnumerable<Product> GetAll() { ... }

      // POST: api/products
      [HttpPost]
      public IActionResult Create(Product product) { ... }

      // PUT: api/products/{id}
      [HttpPut("{id}")]
      public IActionResult Update(int id, Product product) { ... }

      // DELETE: api/products/{id}
      [HttpDelete("{id}")]
      public IActionResult Delete(int id) { ... }
  }
  ```
- In Laravel, the equivalent functionality can be achieved using resource controllers and defining routes in `api.php`.

## HTTP Methods
- **GET**: Retrieve data
- **POST**: Create new resources
- **PUT**: Update existing resources
- **DELETE**: Remove resources

## Attribute Routing
- ASP.NET Core uses attribute routing by decorating controller methods with route attributes.
- Laravel utilizes annotations in routes defined in `routes/api.php`.

## Model Validation with Data Annotations
- In ASP.NET Core, data annotations are used to validate models, e.g., `[Required, StringLength(100)]`.
- Laravel uses validation rules such as `required`, `string|max:100`.

## HTTP Status Codes
- Common status codes include:
  - 200 OK
  - 201 Created
  - 204 No Content
  - 400 Bad Request
  - 404 Not Found
  - 500 Internal Server Error

## JSON Serialization
- ASP.NET Core automatically serializes responses to JSON using System.Text.Json or Newtonsoft.Json. 
- Laravel uses `json()` methods to send JSON responses.

## Error Handling
- ASP.NET Core uses middleware to handle errors globally or specific status codes like 404.
- Laravel employs `app/Exceptions/Handler.php` for customizing the error response.

## Testing with cURL
- Examples:
  - **GET**: `curl -X GET http://localhost:5000/api/products`
  - **POST**: `curl -X POST -H 'Content-Type: application/json' -d '{"name":"Product1"}' http://localhost:5000/api/products`

## Exercises
1. Create a simple REST API with CRUD operations.
2. Implement model validation and error handling.
3. Test the API using cURL commands.

## Reference Links
- [Module 10: Introduction to Web APIs](../module-10)
- [Module 12: Advanced API Development](../module-12)