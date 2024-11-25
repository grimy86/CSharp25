# Anonymous method
We discussed that delegates are used to reference any methods that has the same signature as that of the delegate. In other words, you can call a method that can be referenced by a delegate using that delegate object.

An anonymous method is a method which doesn’t contain any name which is introduced in C# 2.0. It is useful when the user wants to create an inline method and also wants to pass parameter in the anonymous method like other methods. An Anonymous method is defined using the delegate keyword and the user can assign this method to a variable of the delegate type.

```cs
  
public delegate void petanim(string pet); //Delegate

static public void Main() 
{
    // An anonymous method with one parameter 
    petanim p = delegate(string mypet) 
    { 
        Console.WriteLine("My favorite pet is: {0}", mypet); 
    }; 

    p("Dog"); //Function call to an anonymous method
}
```

## Limitations
1. It cannot contain jump statement like goto, break or continue.
2. It cannot access ref or out parameter of an outer method.
3. It cannot have or access unsafe code.
4. It cannot be used on the left side of the is operator.