# Database Access in C#  

## Overview  
In the world of web applications, accessing databases is crucial for storing and retrieving data. C# offers several ORMs and tools for database access, each with its own advantages. This document compares various options available in C# with PHP's PDO, MySQLi, and Eloquent.

## Comparison Table  
| Feature                 | PHP (PDO/MySQLi/Eloquent)      | C# (Entity Framework Core/Dapper)  |  
|-------------------------|----------------------------------|------------------------------------|  
| ORM Support             | Yes (Eloquent)                   | Yes (EF Core, Dapper)             |  
| Connection Strings      | Yes                              | Yes                                |  
| CRUD Operations         | Yes                              | Yes                                |  
| Relationship Support     | One-to-many, Many-to-many       | One-to-many, Many-to-many         |  
| Migrations              | Included (Eloquent), Manual (PDO/MySQLi) | Automatic (EF Core), Manual (Dapper) |  
| Examples                | Available                        | Available                          |  

## DbContext Configuration (Entity Framework Core)  
To use Entity Framework, you need to set up your `DbContext`:

```csharp
public class MyDbContext : DbContext  
{  
    public MyDbContext(DbContextOptions<MyDbContext> options) : base(options) { }  
    public DbSet<User> Users { get; set; }  
    // Other DbSets  
}
```

### Connection String  
To connect to the database, add a connection string in `appsettings.json`:

```json  
{  
  "ConnectionStrings": {  
    "DefaultConnection": "Server=myServerAddress;Database=myDataBase;User Id=myUsername;Password=myPassword;"  
  }  
}
```

## CRUD Operations  
### Create  
```csharp
using (var context = new MyDbContext())  
{  
    var user = new User { Name = "John Doe" };  
    context.Users.Add(user);  
    context.SaveChanges();  
}
```

### Read  
```csharp
var user = context.Users.FirstOrDefault(u => u.Id == userId);
```

### Update  
```csharp
user.Name = "Jane Doe";
context.SaveChanges();
```

### Delete  
```csharp
context.Users.Remove(user);
context.SaveChanges();
```

## Relationships  
### One-to-Many  
Define relationships in DbContext:
```csharp
public class Order  
{  
    public int Id { get; set; }  
    public virtual ICollection<Product> Products { get; set; }  
}
```

### Many-to-Many  
Using a join table:
```csharp
public class Student  
{  
    public int Id { get; set; }  
    public virtual ICollection<Course> Courses { get; set; }  
}
```

## Migrations  
To create migrations, use the following command:
```
dotnet ef migrations add InitialCreate
```

To update the database:
```
dotnet ef database update
```

## Complete Examples  
For a complete implementation, consider checking online resources or build a sample application using the configurations shared.

## Exercises  
1. Implement CRUD operations for a `Product` entity.
2. Create a one-to-many relationship between `Category` and `Product`.
3. Implement a many-to-many relationship using `Student` and `Course`.
4. Create migrations for your database models.
5. Experiment with Dapper for executing raw SQL queries.

## Reference Links  
- [Entity Framework Documentation](https://docs.microsoft.com/en-us/ef/core/)  
- [Dapper Documentation](https://dapper-tutorial.net/)  
- [PHP PDO Documentation](https://www.php.net/manual/en/book.pdo.php)  

### Navigation  
- [Previous Module: Collections and LINQ](06-collections-linq.md)  
- [Next Module: Async Programming](08-async-programming.md)  

## Conclusion  
Understanding database access in C# is crucial for effective application development. By leveraging the right tools, developers can create efficient, maintainable, and powerful applications.