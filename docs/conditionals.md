# Conditionals

## Default Values
Consider [ternary operator](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/null-coalescing-operator) '??' instead of nil checks to improve readability.
```c# title="BAD"
if (name != null)
{
    return name;
}
else
{
    return "John Doe";
}
```
```c# title="GOOD"
return name ?? "John Doe";
```

## Don't Write "if true return true"
When returning or setting a variable to the value of the conditional statement itself, don't use an else block.
```c# title="BAD"
if (name == "mark" || name == "stacy")
{
    return true;
}
else
{
    return false;
}
```
```c# title="GOOD"
return name == "mark" || name == "stacy";
```

## Prefer positive boolean expressions
This ensures that the code remains easy to read.
```c# title="BAD"
if (!isHappy)
{
    return "sad";
}
else
{
    return "happy";
}
```
```c# title="GOOD"
if (isHappy)
{
    return "happy";
}
else
{
    return "sad";
}
```
