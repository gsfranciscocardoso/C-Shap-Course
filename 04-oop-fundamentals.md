# OOP Fundamentals in C# for PHP Developers

## Introduction to OOP
Object-Oriented Programming (OOP) is a programming paradigm that relies on the concept of classes and objects. It allows developers to create modular and reusable code.

## Classes and Objects
A class is a blueprint for creating objects. An object is an instance of a class.

### Example:
```csharp
class Car {
    public string Model;
    public string Color;
    
    public Car(string model, string color) {
        Model = model;
        Color = color;
    }
}
```

## Properties
Properties are used to encapsulate data safely.

### Example:
```csharp
public string Model { get; set; }
```

## Methods
Methods define behaviors of a class.

### Example:
```csharp
public void Drive() {
    Console.WriteLine("Car is driving...");
}
```

## Constructors
A constructor initializes an object.

## Access Modifiers
Access modifiers control visibility. (public, private, protected)

## Namespaces
Namespaces help organize code.

## Static Members
Static members belong to the class rather than instances.

## Exercises
1. Create a class representing a Book.
2. Implement methods to get the details of the book.