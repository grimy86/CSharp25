# Expression-Bodied Members
Expression-bodied members provide a minimal and concise syntax to define properties and methods. It helps to eliminate boilerplate code and helps writing code that is more readable. The expression-bodied syntax can be used when a member’s body consists only of one expression. It uses the =>(fat arrow) operator to define the body of the method or property and allows getting rid of curly braces and the return keyword. The feature was first introduced in C# 6.

## Expression-Bodied Lambda:
```cs
(int x, int y) => x + y;
```

## Expression-Bodied Methods:
Used to define a method with a single expression.
```cs
public int Add(int x, int y) => x + y;
```

## Expression-Bodied Properties:
Define properties with getter-only behavior.
```cs
public int MyProperty => 42;
```

## Expression-Bodied Indexers:
Similar to properties but for indexed access.
```cs
public int this[int index] => index * 2;
```

## Expression-Bodied Constructors, Finalizers, etc.:
Introduced in C# 7.0+ for more concise constructors and destructors.
```cs
public MyClass(string name) => Name = name;
```