# Database Access in C#

## Entity Framework Core
A robust ORM for data access.

### Example:
```csharp
public class AppDbContext : DbContext {
    public DbSet<Car> Cars { get; set; }
}
```

## Dapper
A lightweight ORM.

## Connection Strings
Used for database connections.

## Migrations
Migrations help manage database schema changes.

### Example:
```bash
Add-Migration InitialCreate
Update-Database
```

## Exercises
1. Create a database context for your models.
2. Implement a basic CRUD operation using Entity Framework.