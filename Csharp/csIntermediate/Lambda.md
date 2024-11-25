# Lambda
C# Lambda Expression is a short **block of code that accepts parameters and returns a value**. It is defined as an **anonymous function (function without a name)**.

```cs
num => num * 7 //Expression-bodied lambda
```

Here, num is an input parameter and num * 7 is a return value. The lambda expression **does not execute on its own.** Instead, we use it inside other methods or variables.

## Definition
**Syntax:** (parameterList) => lambda body
- `parameterList` - list of input parameters
- `=>` - a lambda operator
- `lambda body` - can be an expression or statement

## Types of lambda expressions
1. Expression Lambda
2. Statement Lambda

### Expression Lambda or Explicitly typed lambda
Expression lambda contains a single expression in the lambda body.
```cs
(int num) => num * 5;
```

### Statement Lambda or Block-Bodied lambda
Statement lambda encloses one or more statements in the lambda body. We use curly braces `{ }` to wrap the statements.
```cs
(int a, int b) =>
{
    var sum = a + b;
    return sum;
};
```

### Lambda Expression with Delegate
```cs
Func<int, int> multiply = num => num * 3;
```

### **Key Differences Between Expression and Statement Lambdas**
| Feature                      | Expression Lambda                    | Statement Lambda                         |
|------------------------------|--------------------------------------|------------------------------------------|
| Syntax Complexity            | Simple (single expression)           | Supports multiple statements             |
| Implicit Return              | Yes (return type inferred)           | No (must use explicit `return`)          |
| Suitable for                 | Short, single-line logic             | Complex logic requiring multiple lines   |
| Readability                  | High for simple computations         | Better for structured, complex behavior  |

---

### **Best Practices**
- **Use expression lambdas** for concise, straightforward logic.
- **Switch to statement lambdas** when dealing with more complex operations to improve readability and maintainability.
- Explicitly specify parameter types when it aids in clarity or avoids ambiguity.

### Uses
1. Writing Easy and Simple Delegate Code.
2. Performing quick and simple calculations.
3. We can pass a lambda expression as a parameter in a method call.