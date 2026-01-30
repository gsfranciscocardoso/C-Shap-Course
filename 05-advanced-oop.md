# Advanced OOP in C#

## Interfaces
An interface defines a contract for classes.

### Example:
```csharp
public interface IVehicle {
    void Start();
}
```

## Inheritance
Inheritance allows a class to inherit members.

### Example:
```csharp
class ElectricCar : Car {
    public void Charge() {
        Console.WriteLine("Charging...");
    }
}
```

## Polymorphism
Polymorphism enables methods to do different things based on the object type.

### Example:
```csharp
public virtual void DisplayInfo() {
    Console.WriteLine("This is a vehicle.");
}
```

## Abstract Classes
Abstract classes cannot be instantiated.

### Example:
```csharp
public abstract class Vehicle {
    public abstract void Drive();
}
```

## Generics
Generics provide type safety.

## Exercises
1. Create an interface for payment methods.
2. Implement polymorphism using different vehicle types.