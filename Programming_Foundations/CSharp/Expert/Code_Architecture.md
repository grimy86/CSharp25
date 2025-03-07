
- [Software architecture \& design](#software-architecture--design)
  - [Class relationships](#class-relationships)
    - [Association](#association)
    - [Composition](#composition)
    - [Aggregation](#aggregation)
  - [The SOLID principles](#the-solid-principles)
    - [Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
    - [Open/Closed Principle (OCP)](#openclosed-principle-ocp)
    - [Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
    - [Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
    - [Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)
  - [Common Software Architectures](#common-software-architectures)
    - [MVVM (Model-View-ViewModel)](#mvvm-model-view-viewmodel)
    - [MVC (Model-View-Controller)](#mvc-model-view-controller)
    - [MVP (Model-View-Presenter)](#mvp-model-view-presenter)
    - [Layered Architecture (N-Tier)](#layered-architecture-n-tier)
    - [Microservices Architecture](#microservices-architecture)
    - [Event-Driven Architecture](#event-driven-architecture)
    - [Hexagonal (Ports and Adapters) Architecture](#hexagonal-ports-and-adapters-architecture)
    - [Clean Architecture](#clean-architecture)
    - [CQRS (Command-Query Responsibility Segregation)](#cqrs-command-query-responsibility-segregation)
    - [ECS (Entity-Component-System)](#ecs-entity-component-system)
  - [Design patterns](#design-patterns)
    - [Creational design patterns (control object creation)](#creational-design-patterns-control-object-creation)
    - [Structural Design Patterns (control class relationships)](#structural-design-patterns-control-class-relationships)
    - [Behavioral Design Patterns (control object communication)](#behavioral-design-patterns-control-object-communication)

# Software architecture & design

<details>
<summary> Class relationships </summary>

## Class relationships
In object-oriented programming, classes can interact with each other in different ways. The primary relationships between classes are `Association`, `Composition`, and `Aggregation`. Understanding these relationships helps design cleaner, more maintainable code.

### Association
Association is a "uses a" relationship, where one `class uses another` class to perform a task. The classes involved in an association can exist independently. In association, one class might use another class’s methods or behaviors, but neither class owns the other.

Key Points:
- Classes can interact without ownership.
- The lifetime of classes is independent.
- Often implemented via references, pointers, or method parameters.

```cs
public class Student
{
    public int StudentId { get; set; }
    public string FirstName { get; set; }
}

public class StudentRepository
{
    public Student GetStudent(int studentId) // Actively using the Student class
    {
        return new Student();
    }
}
```

### Composition
Composition is a "has a" relationship, where one `class contains a reference to another` class. In this relationship, the containing class (parent) owns the contained class (child). If the parent class is deleted, the child class will also be deleted.

Key Points:
- The parent class owns the child class.
- The child class cannot exist without the parent class.
- Deleting the parent also deletes the child.

Example:
```cs
public class Address
{
    public string Street { get; set; }
    public string City { get; set; }
}

public class Student
{
    public int StudentId { get; set; }
    public Address HomeAddress { get; set; } // Including the Address class
}
```
Here, the Student class owns the Address class. If the Student object is deleted, the `Address object will also be deleted`, indicating a composite relationship.

### Aggregation
Aggregation is a special type of composition, but in this relationship, the `child class can exist independently of the parent class`. The parent class holds a reference to the child class, but the child can live without the parent.

Key Points:
- Aggregation is a "has a" relationship.
- The parent contains a reference to the child, but the child can exist independently.
- Deleting the parent does not delete the child.

Example:
```cs
public class Course
{
    public int CourseId { get; set; }
    public string CourseName { get; set; }
}

public class Student
{
    public int StudentId { get; set; }
    public Course EnrolledCourse { get; set; }
}
```
In this example, the Student class has a reference to the Course class. However, if the Student is deleted, the `Course can still exist independently`, indicating an aggregation relationship.

</details>

<details>
<summary> The SOLID principles </summary>

## The SOLID principles
SOLID is a set of five principles introduced by Robert C. Martin to help create maintainable, scalable, and testable object-oriented software.

These are principles, not design patterns. Principles guide software design, while patterns provide reusable solutions.

- Single Responsibility Principle (SRP): Each class should focus on a single task or responsibility.
- Open/Closed Principle (OCP): You should extend functionality using interfaces, not modifying existing code.
- Liskov Substitution Principle (LSP): Subclasses should follow the behavior of their base classes.
- Interface Segregation Principle (ISP): Interfaces should focus on a single task or responsibility, avoiding class dependency.
- Dependency Inversion Principle (DIP): Depend on interfaces instead of concrete classes.

### Single Responsibility Principle (SRP)
A class should have only one reason to change.

- Each class should focus on a single task or responsibility.
- If a class has multiple responsibilities, split it into smaller classes.

```cs
// ❌ Violating SRP: Handles both data and file operations
public class Report
{
    public string Content { get; set; }
    public void SaveToFile(string path) { /* Saves content to a file */ }
}

// ✔ Following SRP: Separate responsibilities into two classes
public class Report
{
    public string Content { get; set; }
}

public class ReportSaver
{
    public void SaveToFile(Report report, string path) { /* Saves content to a file */ }
}
```

### Open/Closed Principle (OCP)
Software should be open for extension, but closed for modification.

- You should extend functionality without modifying existing code.
- Use inheritance or interfaces to add new behaviors.

```cs
// ❌ Violating OCP: Modifying the existing class to add new behavior
public class PaymentProcessor
{
    public void ProcessPayment(string type)
    {
        if (type == "CreditCard") { /* Process credit card */ }
        else if (type == "PayPal") { /* Process PayPal */ }
    }
}

// ✔ Following OCP: Using abstraction for extensibility
public interface IPaymentMethod { void Pay(); }

public class CreditCardPayment : IPaymentMethod { public void Pay() { /* Credit card logic */ } }
public class PayPalPayment : IPaymentMethod { public void Pay() { /* PayPal logic */ } }

public class PaymentProcessor
{
    public void ProcessPayment(IPaymentMethod paymentMethod) { paymentMethod.Pay(); }
}
```

### Liskov Substitution Principle (LSP)
A subclass should be able to replace its superclass without breaking the program.

- Subclasses should follow the behavior of their base classes.
- Avoid breaking expected behavior when using inheritance.

```cs
// ❌ Violating LSP: Square incorrectly inherits from Rectangle
public class Rectangle
{
    public virtual double Width { get; set; }
    public virtual double Height { get; set; }

    public double Area() => Width * Height;
}

public class Square : Rectangle
{
    public override double Width
    {
        set { base.Width = base.Height = value; } // Unexpected side effect
    }

    public override double Height
    {
        set { base.Width = base.Height = value; } // Unexpected side effect
    }
}

// ✔ Following LSP: Separate Square and Rectangle using a common interface
public interface IShape
{
    double Area();
}

public class RectangleProper : IShape
{
    public double Width { get; set; }
    public double Height { get; set; }
    
    public double Area() => Width * Height;
}

public class SquareProper : IShape
{
    public double Side { get; set; }
    
    public double Area() => Side * Side;
}
```

### Interface Segregation Principle (ISP)
Clients should not be forced to depend on methods they do not use.

- Large interfaces should be split into smaller, more specific ones.
- Classes should only implement the methods they need.

```cs
// ❌ Violating ISP: A printer interface forces all classes to implement every method
public interface IPrinter
{
    void Print();
    void Scan();
    void Fax();
}

public class BasicPrinter : IPrinter
{
    public void Print() { /* Works */ }
    public void Scan() { throw new NotImplementedException(); } // ❌ Unnecessary
    public void Fax() { throw new NotImplementedException(); }  // ❌ Unnecessary
}

// ✔ Following ISP: Split into multiple interfaces
public interface IPrinter { void Print(); }
public interface IScanner { void Scan(); }
public interface IFax { void Fax(); }

public class BasicPrinter : IPrinter { public void Print() { /* Works */ } }
```

### Dependency Inversion Principle (DIP)
High-level modules should not depend on low-level modules. Both should depend on abstractions.

- Depend on interfaces instead of concrete classes.
- Helps with decoupling and makes the code more testable.

```cs
// ❌ Violating DIP: The EmailService directly depends on a concrete class
public class EmailService
{
    private readonly SmtpClient _smtpClient = new SmtpClient(); // Tight coupling
    public void SendEmail() { _smtpClient.Send(); }
}

// ✔ Following DIP: Depend on an abstraction (interface)
public interface IEmailSender { void Send(); }

public class SmtpEmailSender : IEmailSender { public void Send() { /* Email logic */ } }

public class EmailService
{
    private readonly IEmailSender _emailSender;
    public EmailService(IEmailSender emailSender) { _emailSender = emailSender; }
    public void SendEmail() { _emailSender.Send(); }
}
```

</details>


<details>
<summary> Common Software Architectures </summary>

## Common Software Architectures
| Architecture | Best for | Key Benefit |
|-|-|-|
| `MVVM` | WPF, MAUI, Xamarin | Data binding, testability |
| `MVC` | Web apps (ASP.NET, Django) | Scalability, separation |
| `MVP` | WinForms, legacy apps | Easier unit testing |
| `Layered` | Enterprise apps | Clear separation of concerns |
| `Microservices` | Cloud-based, scalable apps | Independent services |
| `Event-Driven` | Real-time, IoT | High responsiveness |
| `Hexagonal` | Large applications | Flexibility, maintainability |
| `Clean` | Scalable systems | Strong separation, longevity |
| `CQRS` | High-performance apps | Optimized read/write ops |
| `ECS` | Game development | Better performance |


### MVVM (Model-View-ViewModel)
MVVM separates the UI (**View**) from the business logic (**ViewModel**) while keeping data and state management in the **Model**.  
- **Used in:** WPF, MAUI, Xamarin  
- **Best for:** Desktop & mobile apps  

**Components:**
- **Model:** Manages data and business logic (e.g., database calls).
- **View:** The UI (XAML in WPF/MAUI).
- **ViewModel:** Acts as a bridge between the View and Model using data binding.

---

### MVC (Model-View-Controller)
The Controller processes user requests (e.g., `/GetUser`), retrieves data from the Model, and passes it to the View.  
- **Used in:** ASP.NET Core, Spring, Django  
- **Best for:** Web apps & APIs  

**Components:**
- **Model:** Handles data and business logic.
- **View:** UI layer (HTML, Razor, or templates).
- **Controller:** Handles user input and updates Model/View.

### MVP (Model-View-Presenter)
Similar to MVVM, but the **Presenter** directly updates the **View** (no data binding like MVVM).  
- **Used in:** WinForms, legacy desktop apps  
- **Best for:** Older desktop applications  

**Components:**
- **Model:** Manages data.
- **View:** Displays UI, but contains no logic.
- **Presenter:** Acts as a mediator between Model and View.

### Layered Architecture (N-Tier)
A structured architecture where components are divided into separate layers.  
- **Used in:** Large applications, enterprise software  
- **Best for:** Scalable web and desktop applications  

**Common Layers:**
1. **Presentation Layer:** UI (Web, desktop, API)
2. **Business Logic Layer (BLL):** Processes data
3. **Data Access Layer (DAL):** Handles database interactions  

### Microservices Architecture
Instead of a single app, multiple **independent services** communicate via **APIs (REST, gRPC)**.  
- **Used in:** Netflix, Amazon, Cloud applications  
- **Best for:** Large, scalable web services  

**Why Use Microservices?**
✅ Scalable  
✅ Independent deployment  
✅ Fault-tolerant  

### Event-Driven Architecture
A system where components react to **events** instead of directly calling each other.  
- **Used in:** IoT, real-time apps, trading systems  
- **Best for:** High-performance, decoupled applications  

**Why Use It?**
✅ Components are loosely coupled  
✅ High responsiveness  
✅ Better scalability  

### Hexagonal (Ports and Adapters) Architecture
Focuses on **isolating core business logic** and keeping dependencies (UI, Database, APIs) **separate**.  
- **Used in:** Scalable applications, long-term projects  
- **Best for:** Maintainable and testable code  

**Why Use It?**
✅ Increased testability  
✅ More flexibility for changing technologies  

### Clean Architecture
A layered design that keeps the **core business logic** at the center, making dependencies flow inward.  
- **Used in:** Large applications  
- **Best for:** Long-term maintainability  

**Why Use It?**
✅ Separation of concerns  
✅ Better dependency management  

### CQRS (Command-Query Responsibility Segregation)
Separates **read operations** from **write operations** to optimize performance.  
- **Used in:** High-performance web apps, financial systems  
- **Best for:** Systems with heavy database operations  

**Why Use It?**
✅ Faster queries  
✅ Scales well with microservices  

### ECS (Entity-Component-System)
A **game development** pattern that replaces traditional OOP hierarchies with a **data-driven approach**.  
- **Used in:** Unity, Unreal Engine  
- **Best for:** Performance-intensive games  

**Why Use It?**
✅ More efficient than OOP  
✅ Better memory management

</details>

<details>
<summary> Design patterns </summary>

## Design patterns
A design pattern is a reusable solution to a common programming problem. It helps make your code more structured, maintainable, and scalable.

- Avoid rewriting code for the same problems.
- Improve code readability and reusability.
- Make your code more flexible to changes.

**Types of design patterns:**
There are three main types of design patterns:
- Creational Patterns: How objects are created.
- Structural Patterns: How objects are structured & connected.
- Behavioral Patterns: How objects interact & communicate.

### Creational design patterns (control object creation)
These patterns provide better ways to control object creation, in a flexible way.

| Pattern |	What it Does | Example Use Case |
|-|-|-|
| Singleton | Ensures only one instance of a class exists. | Database connections, Logging |
| Factory Method | A method creates objects instead of new keyword. | Creating different payment methods (CreditCard, PayPal) |
| Abstract Factory | A factory that creates factories of related objects. | UI toolkit for Windows & Mac |
| Builder | Builds complex objects step by step. | Creating a Burger with different toppings |
| Prototype | Copies an existing object instead of creating a new one. | Copying a user profile |

### Structural Design Patterns (control class relationships)
These patterns deal with how objects are connected and structured.

| Pattern |	What it Does | Example Use Case |
|-|-|-|
| Adapter | Converts one interface into another. | Using an old API in a new system |
| Bridge | Separates abstraction from implementation. | UI themes with different rendering engines |
| Composite | Treats a group of objects like a single object. | Folder structure in Windows Explorer |
| Decorator | Adds extra behavior to objects dynamically. | Adding extra features to a car (e.g., Sunroof) |
| Facade | Provides a simple interface to a complex system. | A single API call to simplify multiple services |
| Flyweight | Uses shared objects to save memory. | Text editors where characters share styles |
| Proxy | Controls access to an object. | Security check before accessing an object |

### Behavioral Design Patterns (control object communication)
These patterns define how objects interact with each other.

| Pattern |	What it Does | Example Use Case |
|-|-|-|
| Chain of Responsibility | Passes a request through a chain of handlers. | Support ticket escalation (Level 1 → Level 2 → Manager) |
| Command | Encapsulates a request as an object. | Undo/Redo in text editors |
| Interpreter | Defines a grammar for interpreting language. | Math expression evaluator |
| Iterator | Provides a way to loop through a collection without exposing details. | Custom collections in C# |
| Mediator | Controls communication between multiple objects. | Chatroom where users communicate via a server |
| Memento | Saves an object's state for undo functionality. | Text editor undo feature |
| Observer | Notifies multiple objects when one object changes. | Stock price alerts |
| State | Changes an object's behavior based on state. | Traffic light system (Red, Yellow, Green) |
| Strategy | Allows switching between different algorithms. | Sorting (BubbleSort, QuickSort) |
| Template | Method	Defines the skeleton of an algorithm in a base class. | Cooking recipes |
| Visitor | Adds extra functionality without modifying existing classes. | Applying a discount to different products |

</details>
