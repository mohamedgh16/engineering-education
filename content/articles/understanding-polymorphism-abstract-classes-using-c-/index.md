### Introduction

According to [Microsoft](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/object-oriented/polymorphism) **Polymorphism** is one of the main concepts in object-oriented programming, after encapsulation and inheritance. *Polymorphism* is a Greek word that means "many-shaped". In any program, objects of a derived class can be used as objects of a base class using functions parameters and collections or arrays.

**Polymorphism** is a very helpful concept when it comes to a single abstract idea used in different ways and shapes. With polymorphism, you can define a single abstract class and reshape it in different ways to suit your methods & ideas. 

### Table of contents

- Understand the concept of polymorphism.
- Understand abstract classes.
- Multiple examples of polymorphism.

### Prerequisites

To follow this article along, you'll need the following:

- A basic understanding of the C# programming language.
- A basic understanding of Inheritance in C# programming language.

If you're new to Inheritance, you should check this tutorial that would help you understand the concept of it [here](https://www.section.io/engineering-education/getting-started-with-inheritance-using-c/).

### Abstract classes

Abstract classes are very simple and generic, and they are always used as base classes. Abstract classes have no meaning on their own, derived classes must be defined to complete the meaning, and they could contain abstract methods or abstract properties.

Basically, *abstract* classes will never be used if not inherited, because they have no meaning on their own, and their variables & methods are useless if not overridden by another inherited classes.

The following example will explain how we can define an abstract class to make a Payroll System Using Polymorphism.

### Worker class

Worker an abstract generic class that will be used later on for the other inherited classes. First, we will define the Constructor, `set()` & `get()` methods of the class.

```C#
public abstract class Worker
{
  private string FSname;
  private string LSname;

  // constructor of class
  public Worker(string FSnameval, string LSnameval)
  {
      FSname = FSnameval;
      LSname = LSnameval;
  }
  // Set & Get for FSname
  public string Fsname
  {
      get
      {
        return Fsname;
      }
      set
      {
        Fsname = value;
      }
  }
  // Set & Get for LSname
  public string Lsname
  {
     get
     {
      return Lsname;
     }
     set
     {
      Lsname = value;
     }
  }
  // return a string of the Worker information
  public override string ToString()
  {
     return FSname + " " + LSname;
  }
  
  // calculating the income of a worker. This is an abstract property that must be defined by the inherited classes.
  public abstract decimal Income();  
}
```

### Chief class

This class will use the previous class and use its properties & methods for the definition of a chief payroll.

```c#
public class Chief : Worker
{
  private decimal salary; 

  // constructor of Chief class
  public Chief(string FSname, string LSname, decimal salary) : base(FSname, LSname)
  {
      Weeklyincome = salary;
  }
  // Get & Set for the Weeklyincome
  public decimal Weeklyincome
  {
     get
     {
      return salary;
     }
     set
     {
      // only positive salary value
      if (value > 0 )
         salary = value;
     }
  }
```

The following piece of code will override the `ToString()` & `Income()` methods.

```c#
  // override worker method to calculate the Income
  public override decimal Income()
  {
    return Weeklyincome;
  }

  // return a string of the Chief information
  public override string ToString()
  {
  return "Chief: " + base.ToString();
  }
}
```
### Commissionemp class

This class will use the main abstract class and use its properties & methods for the definition of a Commission payroll. The following piece of code will define the Constructor of the class, set & get for the `Salary`, `commission` & `amount`.

```C#
public class Commissionemp : Worker
{
   private decimal salary;
   private decimal commission;
   private int amount;

    // constructor of Commissionemp class
    public Commissionemp(string FSname, string LSname, decimal salary, decimal commission, int amount) : base(FSname,LSname)
  {
      Weeklyincome = salary;
      Commission = commission;
      Amount = amount;
  }

  // set & get for Weeklyincome
  public decimal Weeklyincome
  {
    get
    {
      return salary;
    }
    set
    {
      // positive value
      if (value > 0 )
         salary = value;
    }
   }
  // set & get for Commission
  public decimal Commission
  {
    get
    {
      return commission;
    }
    set
    {
      // positive value
      if (value > 0 )
       commission = value;
       }
    }
  // set & get for amount
  public int Amount
  {
    get
    {
      return amount;
    }
    set
    {
      // positive value
      if (value > 0 )
      amount = value;
    }
  }
```

The following piece of code will override the `ToString()` & `Income()` methods from the main class to store the output.

```C#
    // Commissionemp's income.
    public override decimal Income()
    {
        return Weeklyincome + Commission * Amount;
    }
    // return a string of Commissionemp information
    public override string ToString()
    {
      return "Commissionemp: " + base.ToString();
    } 
 } 
```
### Piece_emp class

This class will use the main abstract class and use its properties & methods for the definition of a Piece employee payroll. The following piece of code will define the Constructor of the class, set & get for the `Paymentforpiece` & `amount`.
```C#
public class Piece_emp : Worker 
{
   private decimal Paymentforpiece; 
   private int amount;         

    // constructor of Piece_emp class
    public Piece_emp(string FSname, string LSname, decimal PaymentforP, int amount) : base(FSname,LSname)
    {
       Paymentforpiece = PaymentforP;
       Amount = amount;
    }

    // Set & Get for Paymentforpiece
    public decimal PaymentforP
    {
      get
      {
        return Paymentforpiece;
      }  
      set
      {
        if (value > 0 )
        Paymentforpiece = value;
      }
    }
    // Set & Get for Amount
    public int Amount
    {
      get
      {
        return amount;
      }  
      set
      {
        if (value > 0 )
        amount = value;
      }
    }
```

The following piece of code will override the `ToString()` & `Income()` methods to store the output.
```C#
  //Income of Piece_employee
  public override decimal Income()
  {
    return Amount * Paymentforpiece;
  }

  // return string of Piece_emp information
  public override string ToString()
  {
    return "Piece_emp: " + base.ToString();
  }
}
```

### Polymorphism testing

In main, we will create objects of each worker class we have and output the information of each object to test out each one of them.

```C#
public class Program
{
  public static void Main(string[] args)
  {
      Chief chief = new Chief("Khaled", "Sans", 800);

      Commissionemp Commemp =
      new Commissionemp("Susan", "Jons", 300, 2, 120);

      Piece_emp piece_emp = new Piece_emp("Samir", "Muan",
         Convert.ToDecimal(2.8), 150);
      Worker Worker = chief;

      string output = GetString(Worker) + chief + " earned " +
      chief.Income().ToString("C") + "\n\n";

      Worker = Commemp;
      output += GetString(Worker) + Commemp +
      " earned "+Commemp.Income().ToString("C") + "\n\n";

      Worker = piece_emp;
      output += GetString(Worker) + piece_emp +
      " earned " + piece_emp.Income().ToString("C") +"\n\n";

      Console.WriteLine(output,"Polymorphism in use");
  } 
```

This piece of code will return a string of each worker class.

```C#
  // Worker informations 
  public static string GetString(Worker worker)
  {
    return worker.ToString() + " earned " +
       worker.Income().ToString("C") + "\n";
  }
} 
```

### Polymorphism output

```bash
Boss: Khaled Sans earned $800.00
Boss: Khaled Sans earned $800.00

CommissionWorker: Susan Jons earned $540.00
CommissionWorker: Susan Jons earned $540.00

PieceWorker: samir Muan earned $420.00
PieceWorker: samir Muan earned $420.00
```

### Conclusion
In this tutorial, we have learned about polymorphism and how useful it is when defining a generic abstract idea with different examples & classes, we have also learned how to use an abstract class to define other inherited classes from it. Don't forget to test out and go through the code to completely understand how it works.

### Further reading
1. https://www.section.io/engineering-education/getting-started-with-inheritance-using-c/.
2. https://www.section.io/engineering-education/getting-started-with-windows-forms-using-c-sharp/.
3. https://www.section.io/engineering-education/getting-started-with-game-development-windows-forms/.
