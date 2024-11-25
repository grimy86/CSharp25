# OOP Intermediate
## Pillars of OOP
- Abstraction
- Encapsulation
- Inheritance
- Polymorphism
  
### Abstraction
Hiding unnecessary information and displaying only necessary information.

### Encapsulation
The meaning of Encapsulation, is to make sure that "sensitive" data is hidden from users.
- Declare fields/properties as ``private``
- Declare fields/properties as ``Read-only`` or ``Write-only``
- Provide public get and set methods, through properties, to access and update the value of a private field

### Inheritance
- Base and derived classes
- Method overriding and virtual/override keywords
- Abstract classes and methods
- Interfaces

> [!NOTE]
> C# does not support multiple inheritance.

### Polymorphism
#### Static: Function overloading & Operator overloading
```cs
void print(int i)
{
    Console.WriteLine("Printing int: {0}", i );
}
void print(double f)
{
    Console.WriteLine("Printing float: {0}" , f);
}
```

#### Dynamic: `Abstract` classes & `Virtual` functions
That is because the **base class method overrides the derived class method**, when they share the same name.
However, **C# provides an option to override the base class method**, by adding the virtual keyword to the method inside the base class, and by using the override keyword for each derived class methods:

```cs
abstract class Animal //Base class
{
    // Virtual method
    public virtual void animalSound()
    {
        Console.WriteLine("The animal makes a sound");
    }

    /*
    Data abstraction is the process of hiding certain details and showing only essential information to the user.
    Abstraction can be achieved with either abstract classes or interfaces.
    */
    public abstract void animalSound(); //This is more like a "blueprint".
}

class Dog : Animal  // Derived class (child) 
{
  public override void animalSound() 
  {
    Console.WriteLine("The dog says: bow wow");
  }
}
```

> [!NOTE]
> `Animal myObj = new Animal();`
>
> Will generate an error (Cannot create an instance of the abstract class or interface 'Animal')
