# Module 05: Advanced OOP - Interfaces, Inheritance, Polymorphism & Generics

## Overview

This module covers advanced object-oriented programming concepts in C# with detailed comparisons to PHP. You'll learn about interfaces, inheritance hierarchies, polymorphism, abstract classes, and generics.

## Interfaces

Interfaces define contracts that classes must implement. They specify what a class must do, but not how it does it.

### PHP Interfaces
```php
<?php
interface IPaymentProcessor {
    public function processPayment(float $amount): bool;
    public function refund(string $transactionId): bool;
}

class StripeProcessor implements IPaymentProcessor {
    public function processPayment(float $amount): bool {
        // Stripe implementation
        return true;
    }
    
    public function refund(string $transactionId): bool {
        // Refund logic
        return true;
    }
}

class PayPalProcessor implements IPaymentProcessor {
    public function processPayment(float $amount): bool {
        // PayPal implementation
        return true;
    }
    
    public function refund(string $transactionId): bool {
        // Refund logic
        return true;
    }
}
}
```

### C# Interfaces
```csharp
public interface IPaymentProcessor
{
    bool ProcessPayment(decimal amount);
    bool Refund(string transactionId);
}

public class StripeProcessor : IPaymentProcessor
{
    public bool ProcessPayment(decimal amount)
    {
        // Stripe implementation
        return true;
    }
    
    public bool Refund(string transactionId)
    {
        // Refund logic
        return true;
    }
}

public class PayPalProcessor : IPaymentProcessor
{
    public bool ProcessPayment(decimal amount)
    {
        // PayPal implementation
        return true;
    }
    
    public bool Refund(string transactionId)
    {
        // Refund logic
        return true;
    }
}
```

### Key Differences
- C# interfaces can have default implementations (C# 8+)
- C# supports explicit interface implementation
- PHP uses `implements`, C# uses `:` for both interfaces and inheritance

### Multiple Interface Implementation

**PHP:**
```php
<?php
interface ILoggable {
    public function log(string $message): void;
}

interface ISerializable {
    public function serialize(): string;
}

class User implements ILoggable, ISerializable {
    public function log(string $message): void {
        echo $message;
    }
    
    public function serialize(): string {
        return json_encode($this);
    }
}
```

**C#:**
```csharp
public interface ILoggable
{
    void Log(string message);
}

public interface ISerializable
{
    string Serialize();
}

public class User : ILoggable, ISerializable
{
    public void Log(string message)
    {
        Console.WriteLine(message);
    }
    
    public string Serialize()
    {
        return JsonSerializer.Serialize(this);
    }
}
```

### Default Interface Methods (C# 8+)
```csharp
public interface ILogger
{
    void Log(string message);
    
    // Default implementation
    void LogError(string error)
    {
        Log($"ERROR: {error}");
    }
}

public class ConsoleLogger : ILogger
{
    public void Log(string message)
    {
        Console.WriteLine(message);
    }
    
    // LogError inherited with default implementation
}
```

## Inheritance

Inheritance allows classes to inherit members from a base class, promoting code reuse.

### Single Inheritance

**PHP:**
```php
<?php
class Vehicle {
    protected string $brand;
    protected int $year;
    
    public function __construct(string $brand, int $year) {
        $this->brand = $brand;
        $this->year = $year;
    }
    
    public function getInfo(): string {
        return "{
$this->brand} ({$this->year})";
    }
}

class Car extends Vehicle {
    private int $doors;
    
    public function __construct(string $brand, int $year, int $doors) {
        parent::__construct($brand, $year);
        $this->doors = $doors;
    }
    
    public function getInfo(): string {
        return parent::getInfo() . " - {
$this->doors} doors";
    }
}

$car = new Car("Toyota", 2024, 4);
echo $car->getInfo(); // Toyota (2024) - 4 doors
```

**C#:**
```csharp
public class Vehicle
{
    protected string Brand { get; set; }
    protected int Year { get; set; }
    
    public Vehicle(string brand, int year)
    {
        Brand = brand;
        Year = year;
    }
    
    public virtual string GetInfo()
    {
        return $"{Brand} ({Year})";
    }
}

public class Car : Vehicle
{
    public int Doors { get; set; }
    
    public Car(string brand, int year, int doors) 
        : base(brand, year)  // Call base constructor
    {
        Doors = doors;
    }
    
    public override string GetInfo()
    {
        return $"{base.GetInfo()} - {Doors} doors";
    }
}

var car = new Car("Toyota", 2024, 4);
Console.WriteLine(car.GetInfo()); // Toyota (2024) - 4 doors
```

### Key Differences
- PHP uses `parent::`, C# uses `base`
- C# requires `virtual` keyword in base class and `override` in derived class
- C# uses `: base()` syntax for calling base constructors

## Polymorphism

Polymorphism allows objects of different types to be treated uniformly through a common interface or base class.

### Method Overriding

**PHP:**
```php
<?php
abstract class Animal {
    abstract public function makeSound(): string;
    
    public function describe(): void {
        echo "I am an animal that says: " . $this->makeSound();
    }
}

class Dog extends Animal {
    public function makeSound(): string {
        return "Woof!";
    }
}

class Cat extends Animal {
    public function makeSound(): string {
        return "Meow!";
    }
}

function animalConcert(array $animals): void {
    foreach ($animals as $animal) {
        $animal->describe();
    }
}

$animals = [new Dog(), new Cat()];
animalConcert($animals);
```

**C#:**
```csharp
public abstract class Animal
{
    public abstract string MakeSound();
    
    public void Describe()
    {
        Console.WriteLine($"I am an animal that says: {MakeSound()}");
    }
}

public class Dog : Animal
{
    public override string MakeSound()
    {
        return "Woof!";
    }
}

public class Cat : Animal
{
    public override string MakeSound()
    {
        return "Meow!";
    }
}

void AnimalConcert(List<Animal> animals)
{
    foreach (var animal in animals)
    {
        animal.Describe();
    }
}

var animals = new List<Animal> { new Dog(), new Cat() };
AnimalConcert(animals);
```

### Virtual vs Override

**C# specific:**
```csharp
public class Shape
{
    // Virtual method - can be overridden
    public virtual double CalculateArea()
    {
        return 0;
    }
    
    // Sealed method - cannot be overridden
    public sealed void Display()
    {
        Console.WriteLine($"Area: {CalculateArea()}");
    }
}

public class Circle : Shape
{
    public double Radius { get; set; }
    
    public Circle(double radius)
    {
        Radius = radius;
    }
    
    // Override virtual method
    public override double CalculateArea()
    {
        return Math.PI * Radius * Radius;
    }
}
```

## Abstract Classes

Abstract classes cannot be instantiated and may contain both abstract and concrete methods.

### PHP Abstract Classes
```php
<?php
abstract class Database {
    protected string $connection;
    
    // Abstract method - must be implemented
    abstract protected function connect(): bool;
    abstract protected function query(string $sql): array;
    
    // Concrete method - inherited as-is
    public function disconnect(): void {
        echo "Disconnected from database";
    }
}

class MySQLDatabase extends Database {
    protected function connect(): bool {
        $this->connection = "MySQL connection";
        return true;
    }
    
    protected function query(string $sql): array {
        // MySQL query implementation
        return [];
    }
}

class PostgreSQLDatabase extends Database {
    protected function connect(): bool {
        $this->connection = "PostgreSQL connection";
        return true;
    }
    
    protected function query(string $sql): array {
        // PostgreSQL query implementation
        return [];
    }
}
```

### C# Abstract Classes
```csharp
public abstract class Database
{
    protected string Connection { get; set; }
    
    // Abstract methods - must be implemented
    protected abstract bool Connect();
    protected abstract List<object> Query(string sql);
    
    // Concrete method - inherited as-is
    public void Disconnect()
    {
        Console.WriteLine("Disconnected from database");
    }
}

public class MySQLDatabase : Database
{
    protected override bool Connect()
    {
        Connection = "MySQL connection";
        return true;
    }
    
    protected override List<object> Query(string sql)
    {
        // MySQL query implementation
        return new List<object>();
    }
}

public class PostgreSQLDatabase : Database
{
    protected override bool Connect()
    {
        Connection = "PostgreSQL connection";
        return true;
    }
    
    protected override List<object> Query(string sql)
    {
        // PostgreSQL query implementation
        return new List<object>();
    }
}
```

### Abstract Classes vs Interfaces

| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| Can have implementation | Yes | Yes (C# 8+) |
| Can have fields | Yes | No |
| Can have constructors | Yes | No |
| Multiple inheritance | No | Yes |
| Access modifiers | Yes | Public only (members) |

**When to use what:**
- **Abstract Class**: When classes share common implementation and state
- **Interface**: When defining a contract that unrelated classes can implement

## Generics

Generics provide type safety and code reuse without sacrificing performance.

### PHP Generics (via DocBlocks - not enforced)
```php
<?php
/**
 * @template T
 */
class Repository {
    private array $items = [];
    
    /**
     * @param T $item
     */
    public function add($item): void {
        $this->items[] = $item;
    }
    
    /**
     * @return T[]
     */
    public function getAll(): array {
        return $this->items;
    }
}

// Not type-safe at runtime
$userRepo = new Repository();
$userRepo->add(new User());
$userRepo->add("Not a user"); // Allowed, but shouldn't be
```

### C# Generics (Enforced at Compile Time)
```csharp
public class Repository<T>
{
    private List<T> items = new List<T>();
    
    public void Add(T item)
    {
        items.Add(item);
    }
    
    public List<T> GetAll()
    {
        return items;
    }
}

// Type-safe!
var userRepo = new Repository<User>();
userRepo.Add(new User());
// userRepo.Add("Not a user");  // Compile error!

var productRepo = new Repository<Product>();
productRepo.Add(new Product());
```

### Generic Constraints

```csharp
// Constraint: T must be a class
public class Container<T> where T : class
{
    private T item;
}

// Constraint: T must implement IComparable
public class SortedList<T> where T : IComparable<T>
{
    public void Sort() { /* ... */ }
}

// Multiple constraints
public class Repository<T> 
    where T : class, IEntity, new()
{
    public T CreateNew()
    {
        return new T();  // new() constraint allows instantiation
    }
}
```

### Generic Methods

```csharp
public class Utilities
{
    // Generic method
    public static T Max<T>(T first, T second) 
        where T : IComparable<T>
    {
        return first.CompareTo(second) > 0 ? first : second;
    }
    
    // Generic method with multiple type parameters
    public static TOutput Convert<TInput, TOutput>(TInput input)
    {
        // Conversion logic
        return (TOutput)(object)input;
    }
}

// Usage
int maxInt = Utilities.Max(10, 20);
string maxString = Utilities.Max("apple", "banana");
```

### Sealed Classes and Methods

C# allows you to prevent inheritance using the `sealed` keyword.

```csharp
// Sealed class - cannot be inherited
public sealed class Configuration
{
    public string ConnectionString { get; set; }
}

// This won't compile:
// public class MyConfig : Configuration { }

// Sealed method - cannot be overridden in derived classes
public class Vehicle
{
    public virtual void Start() { }
}

public class Car : Vehicle
{
    public sealed override void Start() 
    {
        Console.WriteLine("Car starting...");
    }
}

public class SportsCar : Car
{
    // Cannot override Start() - it's sealed
    // public override void Start() { }  // Compile error
}
```

## Reference Links

- [C# Interfaces](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/types/interfaces)
- [Inheritance in C#](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/object-oriented/inheritance)
- [Polymorphism](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/object-oriented/polymorphism)
- [Abstract Classes](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members)
- [Generics](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/types/generics)
- [Generic Constraints](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/constraints-on-type-parameters)

## Exercises

### Exercise 1: Interface Design
Create a file storage system with the following requirements:
1. Create an `IFileStorage` interface with methods: `Upload`, `Download`, `Delete`
2. Implement two classes: `LocalFileStorage` and `CloudFileStorage`
3. Create a `FileManager` class that accepts any `IFileStorage` implementation

### Exercise 2: Inheritance Hierarchy
Build a simple e-commerce system:
1. Create a base `Product` class with common properties (Name, Price, Description)
2. Create derived classes: `PhysicalProduct` (add Weight, Dimensions) and `DigitalProduct` (add DownloadUrl, FileSize)
3. Override `ToString()` method in each class to provide specific information

### Exercise 3: Polymorphism in Action
Create a notification system:
1. Create an abstract `Notification` class with abstract method `Send()`
2. Implement `EmailNotification`, `SmsNotification`, and `PushNotification`
3. Create a `NotificationService` that accepts a list of `Notification` objects and sends them all

### Exercise 4: Generic Repository
Implement a generic repository pattern:
1. Create a generic `Repository<T>` class with CRUD operations
2. Add constraints so `T` must implement an `IEntity` interface (with `Id` property)
3. Test with different entity types (User, Product, Order)

### Exercise 5: Abstract Class vs Interface
Analyze and implement:
1. Create an abstract `PaymentMethod` class with some common implementation
2. Create an `IRefundable` interface for payment methods that support refunds
3. Implement `CreditCardPayment` (extends PaymentMethod, implements IRefundable)
4. Implement `CashPayment` (extends PaymentMethod, does NOT implement IRefundable)

## Solutions

Solutions can be found in [/exercises/05-advanced-oop/](./exercises/05-advanced-oop/)

---

**Previous**: [04 - OOP Fundamentals](./04-oop-fundamentals.md) | **Next**: [06 - Collections and LINQ](./06-collections-linq.md)