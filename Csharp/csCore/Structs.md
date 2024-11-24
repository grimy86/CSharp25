# Structures
In C#, a structure is a value type data type. It helps you to make a single variable hold related data of various data types. The struct keyword is used for creating a structure.

Structures are used to represent a record.

```cs
//Defining a struct
struct Books {
   public string title;
   public string author;
   public string subject;
   public int book_id;
};

//Declaring a struct
Books Book1;
Book1.title = "C Programming";
Book1.author = "Nuha Ali"; 
Book1.subject = "C Programming Tutorial";
Book1.book_id = 6495407;

//Using the struct
Console.WriteLine( "Book 1 title : {0}", Book1.title);
```

>[!NOTE]
> - classes are reference types and structs are value types
> - structures do not support inheritance
> - structures cannot have default constructor

