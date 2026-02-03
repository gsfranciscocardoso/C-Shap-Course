# C# Best Practices

## Naming Conventions
- **Classes:** Use PascalCase. E.g., `CustomerInfo`
- **Methods:** Use PascalCase. E.g., `GetCustomerData()`
- **Variables:** Use camelCase. E.g., `customerName`

## SOLID Principles
1. **S**ingle Responsibility Principle: A class should have one reason to change.
2. **O**pen/Closed Principle: Classes should be open for extension but closed for modification.
3. **L**iskov Substitution Principle: Objects should be replaceable with instances of their subtypes.
4. **I**nterface Segregation Principle: No client should be forced to depend on methods it does not use.
5. **D**ependency Inversion Principle: High-level modules should not depend on low-level modules, but both should depend on abstractions.

## Code Organization
- Group related classes in namespaces.
- Use folders to separate components, models, services, etc.

## Design Patterns
- **Singleton:** Ensures a class has only one instance.
- **Factory Method:** Creates objects without specifying the exact class.
- **Observer:** Allows a way to notify multiple objects about state changes.

## Error Handling
- Use exceptions to handle errors gracefully.
- Implement try-catch blocks for critical code paths.

## Performance Tips
- Prefer `StringBuilder` over string concatenation for performance.
- Use asynchronous programming with `async` and `await` for I/O-bound tasks.

## Security Practices
- Validate input to avoid injection attacks.
- Use HTTPS for secure communication.

## Comparisons with PHP
- **Typing:** C# is statically typed; PHP is dynamically typed. 
- **Error Handling:** C# uses exceptions, while PHP relies on warnings/notices as well as exceptions.

## Navigation
- [Back to Module 13: Unit Testing](13-unit-testing.md)
- [Back to README](README.md)