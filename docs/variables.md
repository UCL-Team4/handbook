# Variables

## Naming

### Name constants using ALL_CAPS
In C#, constants are named using ALL_CAPS with underscores separating words.
`const` keyword is used for constant values, and `readonly` can be used for values that are set once and do not change after.

```c#
const string MY_CONSTANT = "constant value";
public static readonly string MY_GLOBAL_CONSTANT = "another constant value";
```

### camelCase for non-constant local variable names
Local variables should follow camelCase to enhance readability and distinguish them from global or class-level variables.

```c#
string myVariable = "variable value";
```

### PascalCase for public properties and global variables
For global or public variables and properties, use PascalCase. This convention helps differentiate properties and fields from local variables.

```c#
public string MyGlobalVariable = "global variable value";
```

## Use underscore "_" for unused variables in lambda expressions
In C#, use _ to indicate variables that are required syntactically but will not be used.
This is commonly seen in lambda expressions or event handlers.

```c#
public void PrintValues(Dictionary<int, string> map)
{
    foreach (var (_, value) in map)
    {
        Console.WriteLine(value);
    }
}
```

## Enums Vs Booleans
Enums should be used to represent a state when more than two options exist.
Using multiple booleans to reflect different states can lead to confusion and unintended states. For example:


```c# title="BAD"
bool isWalking = false;
bool isRunning = false;
```

Instead, use an enum to represent the state clearly:

```c# title="GOOD"
public enum MovementState
{
    Unknown = 0,
    Walking = 1,
    Running = 2
}

MovementState movementState = MovementState.Unknown;
```

Using an enum simplifies state management and future expansion (e.g., adding Idle, Swimming, etc.) while avoiding ambiguous states.

## Location

### Local Variables: Declare variables within a method as close as possible to where they’re used.
This minimizes the cognitive load for anyone reading the code, as they only need to consider relevant variables.

### Class-Level Variables: Declare at the top of the class in the order: constants, readonly fields, private variables, and then public properties.
This keeps the structure organized and consistent.

### Global Variables: Avoid unnecessary global variables. If needed, declare them at the top of the file and only within a single, relevant file (client or server).
This keeps the code organized and prevents variables from being scattered across multiple locations.
