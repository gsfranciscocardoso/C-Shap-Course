# Comprehensive Unit Testing Guide

## Introduction
Unit testing is a crucial part of software development, ensuring that individual components of your application function correctly. This guide focuses on using xUnit in C#, the Moq mocking framework, and comparisons with PHP's PHPUnit.

## xUnit Basics
### Fact and Theory Attributes
Using xUnit, we can structure our unit tests using two main attributes: `Fact` and `Theory`.

#### Example of Fact
```csharp
[Fact]
public void Addition_ShouldReturnCorrectSum()
{
    int result = 2 + 3;
    Assert.Equal(5, result);
}
```
### Example of Theory
```csharp
[Theory]
[InlineData(2, 3, 5)]
[InlineData(5, 5, 10)]
public void Addition_ShouldReturnExpectedSum(int x, int y, int expected)
{
    int result = x + y;
    Assert.Equal(expected, result);
}
```

## Mocking with Moq
Moq is a powerful mocking framework for .NET. It allows you to create mock objects and set up various behaviors.

### Setup Example
```csharp
var mockRepository = new Mock<IRepository>();
mockRepository.Setup(repo => repo.GetAll()).Returns(new List<Item> { new Item() });
```
### Verify Example
```csharp
mockRepository.Verify(repo => repo.GetAll(), Times.Once);
```

## AAA Pattern
The Arrange-Act-Assert (AAA) pattern is a best practice for structuring unit tests.
1. **Arrange:** Set up the test data and environment.
2. **Act:** Execute the method under test.
3. **Assert:** Verify the result.

### Example
```csharp
[Fact]
public void ShouldReturnItem_WhenItemExists()
{
    // Arrange
    var mockRepository = new Mock<IRepository>();
    mockRepository.Setup(repo => repo.GetById(1)).Returns(new Item());

    var service = new ItemService(mockRepository.Object);

    // Act
    var result = service.GetItem(1);

    // Assert
    Assert.NotNull(result);
}
```

## Comparison with PHP PHPUnit
While both xUnit and PHPUnit serve similar purposes, their syntax and usage patterns differ. Unit tests in PHPUnit are structured somewhat differently:

### PHPUnit Example
```php
public function testAddition()
{
    $this->assertEquals(5, 2 + 3);
}
```

## Exercises
1. Write unit tests for the `ItemService` class.
2. Implement and test a method that adds two numbers utilizing the AAA pattern.

## Navigation
- [Module 12: Dependency Injection](12-dependency-injection.md)
- [Module 14: Best Practices](14-best-practices.md)

---
This comprehensive guide aims to set you on the path to mastering unit testing in your applications. Happy coding!