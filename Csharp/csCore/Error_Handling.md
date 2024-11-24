# Exception handling
The throw statement is used together with an exception class. Exceptions are types that all ultimately derive from **System.Exception**.

There are many exception classes available in C#:
- ArithmeticException
- FileNotFoundException
- IndexOutOfRangeException
- TimeOutException, etc

```cs
//We won't cover try, catch & finally
if (age < 18)
  {
    throw new ArithmeticException("Access denied - You must be at least 18 years old.");
  }
```

## Creating User-Defined Exceptions
1. Your class has to inherit from System.Exception
2. Make sure the class is serializable, add the [Serializable] attribute
3. Provide common exception constructors
```cs
[Serializable]
public class MyException : Exception
{
    public MyException ()
    {}

    public MyException (string message) 
        : base(message)
    {}

    public MyException (string message, Exception innerException)
        : base (message, innerException)
    {}    
}
```