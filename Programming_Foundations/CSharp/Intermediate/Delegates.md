# Delegates
A delegate is a reference type **variable that holds the reference to a method**. The reference can be changed at runtime. Similar to **pointers to functions**, in C or C++.

There are three steps involved while working with delegates:
- Declare a delegate
- Create an instance and reference a method
- Invoke a delegate

```cs
//Declaration
public delegate void MyDelegate(string msg);

//Instantiation & referencing
MyDelegate del = new MyDelegate(MethodA);
// or 
MyDelegate del = MethodA; 
// or set lambda expression 
MyDelegate del = (string msg) =>  Console.WriteLine(msg);

// target method
static void MethodA(string message) //Notice how the function parameters match the delegate signature.
{
    
    Console.WriteLine(message);
}

//Invocation
del.Invoke("Hello World!");
// or 
del("Hello World!");
```
![delegates](/Programming_Foundations/CSharp/Images/Delegates.png)

# Passing delegates
```cs
static void InvokeDelegate(MyDelegate del) // MyDelegate type parameter
    {
        del("Hello World");
    }
```

# Multicast Delegate
The delegate can **point to multiple methods**. A delegate that points multiple methods is called a multicast delegate.

This is done by adding functions to an invocation list using operators:
- `+`, add a function to the list
- `+=`, add a function to the list
- `-`, remove a function from the list
- `-=`, remove a function from the list

```cs
class Program
{
    static void Main(string[] args)
    {
        MyDelegate del1 = ClassA.MethodA;
        MyDelegate del2 = ClassB.MethodB;

        MyDelegate del = del1 + del2; // combines del1 + del2
        del("Hello World");

        MyDelegate del3 = (string msg) => Console.WriteLine("Called lambda expression: " + msg);
        del += del3; // combines del1 + del2 + del3
        del("Hello World");

        del = del - del2; // removes del2
        del("Hello World");

        del -= del1 // removes del1
        del("Hello World");
    }
}

class ClassA
{
    static void MethodA(string message)
    {
        Console.WriteLine("Called ClassA.MethodA() with parameter: " + message);
    }
}

class ClassB
{
    static void MethodB(string message)
    {
        Console.WriteLine("Called ClassB.MethodB() with parameter: " + message);
    }
}
```

# Generic delegates
A generic delegate can be defined the same way as a delegate but using generic type parameters or return type. The generic type must be specified when you set a target method.

```cs
public delegate T add<T>(T param1, T param2); // generic delegate
```

# Func, Action And Predicate delegates
Whenever we use delegates, we have to declare a delegate, initialize it, and then call a method with a reference variable.

In order to get rid of all the first steps, we can directly use Func, Action, or Predicate delegates.

- The Func delegate takes zero, one or more input parameters, and returns a value (with its out parameter).
- The action takes zero, one or more input parameters, but does not return anything.
- Predicate is a special kind of Func. It represents a method that contains a set of criteria mostly defined inside an if condition and checks whether the passed parameter meets those criteria or not.
- 
## Use cases
1. Event Handling
2. Callback Methods
3. Encapsulation of Methods
4. LINQ and Functional Programming
5. Dynamic Behavior at Runtime
6. Multicasting
7. Custom Implementations of Patterns
   -  Observer pattern (This is how events work in C#)
   -  Strategy pattern
   -  Command pattern
   -  Template Method pattern
   -  Decorator pattern
   -  Factory Method pattern
   -  Chain of Responsibility pattern
   -  ...