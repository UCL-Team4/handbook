# Methods

## Size & Scope
- Functions should only do one thing and should be small. If a function is not small, break it up into smaller functions.
- Avoid mixing high-level code with low-level code in the same function.


```c# title="BAD"
// BAD: This function does too much and mixes high- and low-level logic
decimal ApplyDiscount(Customer customer, decimal price)
{
    // High-level: Validate input
    if (customer == null || price <= 0)
    {
        throw new ArgumentException("Invalid customer or price");
    }

    // Low-level: Calculate discount
    decimal discount = customer.IsMember ? price * 0.1m : 0;

    // High-level: Apply discount
    return price - discount;
}

```

```c# title="GOOD"
// GOOD: Each function does one thing, and responsibilities are separated
decimal ApplyDiscount(Customer customer, decimal price)
{
    ValidateInput(customer, price);
    decimal discount = CalculateDiscount(customer, price);
    return price - discount;
}

void ValidateInput(Customer customer, decimal price)
{
    if (customer == null || price <= 0)
    {
        throw new ArgumentException("Invalid customer or price");
    }
}

decimal CalculateDiscount(Customer customer, decimal price)
{
    return customer.IsMember ? price * 0.1m : 0;
}
```


## Naming
- Local functions should be named in camelCase format to differentiate them from standard library methods.
- Public or global functions should be named in PascalCase format.
- Functions should also be named with a leading verb.

```c# title="BAD"
void Player() { }
void PlayerDrop() { }
```
```c# title="GOOD"
void GetPlayerObject() { }
void DropPlayer() { }
```

## Parameters

### Limit Number of Parameters
If needing more than 3 or so parameters for a single method, consider grouping the parameters within a class or struct.
This enhances readability and makes the method easier to manage.


```c# title="BAD"
void CreateCharacter(string name, int age, double height, DateTime birthday, string nationality) { }
```
// BAD
void CreateCharacter(string name, int age, double height, DateTime birthday, string nationality) { }

```c# title="GOOD"
public class Character
{
    public string Name { get; set; }
    public int Age { get; set; }
    public double Height { get; set; }
    public DateTime Birthday { get; set; }
    public string Nationality { get; set; }
}

void CreateCharacter(Character character) { }
```



## Optional Parameters
### Required parameters should come before optional ones.

```c# title="BAD"
void PrintMessage(bool isUrgent = false, string message)
{
    Console.WriteLine(isUrgent ? "URGENT: " + message : message);
}
```
```c# title="GOOD"
void PrintMessage(string message, bool isUrgent = false)
{
    Console.WriteLine(isUrgent ? "URGENT: " + message : message);
}
```


## Use Guard Clauses
### Often, before doing the "real" work of a method, certain pre-conditions must be met.
Guard clauses are conditional statements that provide early returns to check these conditions,
allowing for early exits and reducing nesting, which improves readability.


```c# title="BAD"
string GetFullName(string firstName, string lastName)
{
    if (!nameHidden && firstName != null && lastName != null)
    {
        return firstName + " " + lastName;
    }
    else
    {
        return null;
    }
}

```
```c# title="GOOD"
string GetFullName(string firstName, string lastName)
{
    if (nameHidden) return null;
    if (firstName == null || lastName == null) return null;
    return firstName + " " + lastName;
}
```