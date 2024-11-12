# Unit Test

## Red Green Refactor
The Red-Green-Refactor cycle is a way to develop software incrementally and iteratively. It is a core practice of Test-Driven Development (TDD) and is used to ensure that the code is working correctly and efficiently.

### Red Phase (Failing Test)
Begin by writing a test for the functionality you plan to implement. At this point, the test should fail since the functionality does not yet exist or isn’t complete.

This Red Phase ensures that the test is valid and will catch issues if the implementation is incorrect.

```c#
[TestMethod]
public void TestCalculateTotal_WhenNoItems_ShouldReturnZero()
{
    // Arrange
    var cart = new ShoppingCart();

    // Act
    var result = cart.CalculateTotal();

    // Assert
    Assert.AreEqual(0, result); // Test fails initially, as CalculateTotal is not yet implemented
}
```


### Green Phase (Passing Test)
Implement the minimum amount of code required to make the test pass. Do only as much as needed to pass the test.

This step is focused on meeting the requirements set by the test, not on optimizing or refining the code.

```c#
public class ShoppingCart
{
    public decimal CalculateTotal()
    {
        return 0; // Initial code to make the test pass
    }
}
```

### Refactor Phase
Once the test passes, refactor the code to improve its design, readability, and maintainability. This phase ensures that the code is clean, efficient, and follows best practices.

The goal is to ensure the code adheres to best practices and is optimized while still passing the test.

```c#
public class ShoppingCart
{
    private List<Item> items = new List<Item>();

    public decimal CalculateTotal()
    {
        return items.Sum(item => item.Price); // Refactored to handle multiple items
    }
}
```

## How to write a good unit test

### 1. Use Clear and Descriptive Names
A test name should clearly describe the scenario being tested and the expected outcome. This helps anyone reading the code understand what the test checks without needing to dive into its details.

```c# title="BAD"
[TestMethod]
public void Test1()
{
    var result = new ShoppingCart().CalculateTotal();
    Assert.AreEqual(0, result);
}
```

```c# title="GOOD"
[TestMethod]
public void CalculateTotal_WhenCartIsEmpty_ShouldReturnZero()
{
    // Arrange
    var cart = new ShoppingCart();

    // Act
    var result = cart.CalculateTotal();

    // Assert
    Assert.AreEqual(0, result);
}
```

### 2. Follow the AAA Pattern (Arrange, Act, Assert)
The AAA pattern helps structure the test into three distinct sections: Arrange, Act, and Assert.

```c# title="BAD"
[TestMethod]
public void TestCalculateTotal()
{
    Assert.AreEqual(30, new ShoppingCart { Items = { new Item(10), new Item(20) } }.CalculateTotal());
}
```
```c# title="GOOD"
[TestMethod]
public void CalculateTotal_WithItems_ShouldReturnSumOfPrices()
{
    // Arrange
    var cart = new ShoppingCart();
    cart.AddItem(new Item { Price = 10 });
    cart.AddItem(new Item { Price = 20 });

    // Act
    var result = cart.CalculateTotal();

    // Assert
    Assert.AreEqual(30, result);
}
```

### 3. Test One Scenario At A Time
Each test should focus on one specific scenario or behavior. Testing multiple behaviors in a single test makes it harder to diagnose the issue when it fails.

```c# title="BAD"
[TestMethod]
public void CalculateTotal_WithEmptyCartAndWithItems_ShouldReturnCorrectResult()
{
    var cart = new ShoppingCart();
    Assert.AreEqual(0, cart.CalculateTotal());

    cart.AddItem(new Item { Price = 15 });
    Assert.AreEqual(15, cart.CalculateTotal());
}
```

```c# title="GOOD"
[TestMethod]
public void CalculateTotal_WhenCartIsEmpty_ShouldReturnZero()
{
    var cart = new ShoppingCart();
    var result = cart.CalculateTotal();
    Assert.AreEqual(0, result);
}

[TestMethod]
public void CalculateTotal_WithSingleItem_ShouldReturnItemPrice()
{
    var cart = new ShoppingCart();
    cart.AddItem(new Item { Price = 15 });
    var result = cart.CalculateTotal();
    Assert.AreEqual(15, result);
}
```

### 4. Make Tests Independent
A unit test should be independant of other tests, therefore, each test should not rely on the state of another test. This ensures that each test can be run in isolation without affecting the results.

```c# title="BAD"
[TestMethod]
public void CalculateTotal_WithMultipleCalls_ShouldReturnCumulativeTotal()
{
    var cart = new ShoppingCart();
    cart.AddItem(new Item { Price = 10 });
    Assert.AreEqual(10, cart.CalculateTotal());

    cart.AddItem(new Item { Price = 20 });
    Assert.AreEqual(30, cart.CalculateTotal());
}
```

```c# title="GOOD"
[TestMethod]
public void CalculateTotal_AfterAddingMultipleItems_ShouldReturnSumOfPrices()
{
    var cart = new ShoppingCart();
    cart.AddItem(new Item { Price = 10 });
    cart.AddItem(new Item { Price = 20 });

    Assert.AreEqual(30, cart.CalculateTotal());
}
```