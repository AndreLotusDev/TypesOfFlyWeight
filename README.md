# Flyweight Pattern in C#

## Introduction
The Flyweight Pattern is a structural design pattern that focuses on reducing the number of objects created, to decrease memory footprint and increase performance. This pattern is particularly useful when a large number of similar objects are used. It works by sharing as much data as possible with other similar objects; in other words, it is used to minimize memory usage by sharing as much data as possible with other similar objects.

## Flyweight Pattern Concept
In the Flyweight pattern, instead of creating large numbers of similar objects, objects are reused. A common interface allows the flyweight objects to receive and act on extrinsic state passed by client code.

### When to Use
- When an application uses a large number of objects
- When the storage costs are high due to a vast quantity of objects
- When the application does not depend on object identity

## Implementation in C#
Below is an example implementation of the Flyweight Pattern in C#. In this example, we demonstrate a simple context where the Flyweight pattern can be applied.

### Flyweight Class
This is a shared class whose instances are going to be reused.

```csharp
public class Flyweight
{
    private readonly string _intrinsicState;

    public Flyweight(string intrinsicState)
    {
        _intrinsicState = intrinsicState;
    }

    public void Operation(string extrinsicState)
    {
        Console.WriteLine($"Flyweight: Intrinsic state {_intrinsicState}, Extrinsic state {extrinsicState}");
    }
}
```

### Flyweight Factory
This class creates and manages flyweight objects and ensures that flyweights are shared properly.

```csharp
public class FlyweightFactory
{
    private Dictionary<string, Flyweight> _flyweights = new Dictionary<string, Flyweight>();

    public Flyweight GetFlyweight(string key)
    {
        if (!_flyweights.ContainsKey(key))
        {
            _flyweights[key] = new Flyweight(key);
        }

        return _flyweights[key];
    }
}
```

### Client Code
Here's an example of how a client might use these classes:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var factory = new FlyweightFactory();

        var flyweightA = factory.GetFlyweight("A");
        var flyweightB = factory.GetFlyweight("B");
        var flyweightC = factory.GetFlyweight("A"); // Reuses existing instance

        flyweightA.Operation("1");
        flyweightB.Operation("2");
        flyweightC.Operation("3"); // Notice that this reuses flyweightA's intrinsic state
    }
}
```

## Conclusion
The Flyweight pattern is a powerful tool for optimizing resource usage in software that deals with a large number of similar objects. By sharing common parts of the state between objects, it can significantly reduce the memory footprint of an application.
