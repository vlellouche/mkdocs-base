﻿# More on Classes
In this chapter, we explained classes and instances. So before we start we create a new class 'ClassesAndInstances.cs' inside Training folder and call it into the menu 'Classes and Instances'

ClassesAndInstances.cs :
```diff
+ using System.Windows.Forms;
namespace Northwind.Training
{
    class ClassesAndInstances
    {
+       public void Run()
+       {
+       }     
    }
}
```

ApplicationMdi.cs
```diff
private void classesAndInstancesToolStripMenuItem_Click(object sender, EventArgs e)
{
	new Training.ClassesAndInstances().Run();
}
```

A class is a collection of operations and data, we want demonstrating in an other class it calls it Animal.cs and we put some informations on this class with a member

```diff
namespace Northwind.Training
{
    class Animal
    {
+       public void Run()
+       {
+           public string Name;
+       }     
    }
}
```

And go back to ClassesAndInstances.cs

```diff
using System.Windows.Forms;
namespace Northwind.Training
{
    class ClassesAndInstances
    {
       public void Run()
       {
+            Animal a = new Animal();
+            Animal b = new Animal();
+            a.Name = "Rex";
+            b.Name = "Kitty";
+            MessageBox.Show(a.Name); 
+            MessageBox.Show(b.Name); 
       }     
    }
}
```
Build it and run it, you have two messages box are opening with Rex then Kitty.
By doing a `new Animal()`, we define a new object in the memory, a new instance of the class Animal
Creating a instance allows you to separate or organize your data in your code. Now, you can add an other property as:
 Animal.cs
 ```diff
namespace Northwind.Training
{
    class Animal
    {
       public void Run()
       {
           public string Name;
+          public string AnimalType;
       }     
    }
}
```

ClassesAndInstances.cs

```diff
using System.Windows.Forms;
namespace Northwind.Training
{
    class ClassesAndInstances
    {
       public void Run()
       {
            Animal a = new Animal();
            Animal b = new Animal();
            a.Name = "Rex";
+           b.AnimalType = "Dog" ;
            b.Name = "Kitty";
+           b.AnimalType = "Cat" ;
-           MessageBox.Show(a.Name); 
+           MessageBox.Show(a.Name+" is a "+a.AnimalType); 
-            MessageBox.Show(b.Name); 
+           MessageBox.Show(b.Name+" is a "+b.AnimalType); 
       }     
    }
}
```
Build it, run it, and check you received two message box "Rex is a Dog" and "Kitty is a Cat".
Go back to the Animal class, and declare a method who return the message box.
 Animal.cs
 ```diff
+ using System.Windows.Forms;
namespace Northwind.Training
{
    class Animal
    {
       public void Run()
       {
           public string Name;
           public string AnimalType;
+          public void DescribeYourSelf()
+          {
+           MessageBox.Show(this.Name+" is a "+this.AnimalType); 
+          }  
       }     
    }
}
```
`this` is referencing to the current instance of the Animal class, so now you can write 
ClassesAndInstances.cs

```diff
using System.Windows.Forms;
namespace Northwind.Training
{
    class ClassesAndInstances
    {
       public void Run() 
       {
            Animal a = new Animal();
            Animal b = new Animal();
            a.Name = "Rex";
            b.AnimalType = "Dog" ;
            b.Name = "Kitty";
            b.AnimalType = "Cat" ;
-           MessageBox.Show(a.Name+" is a "+a.AnimalType); 
+           a.DescribeYourSelf();
-           MessageBox.Show(b.Name+" is a "+b.AnimalType); 
+           b.DescribeYourSelf();
       }     
    }
}
```

In brief, we moved the logic description from the outside code into the Animal class itself.

<iframe width="560" height="315" src="https://www.youtube.com/embed/v6wbQgPYwU0?list=PL1DEQjXG2xnKI3TL-gsy91eXbh3ytOt6h" frameborder="0" allowfullscreen></iframe>

# More on Classes constructor static and readonly

So we saw previously, we created member name `a` and `b` of type `Animal` and assign it with a new instance of `Animal()`.
For define a new instance of a class, you are calling a special method called the **Constructor** and if we don't define a constructor then automatically want to get created for us.
A constructor cannot return a value to the calling code and is name is the same name of the class that you use.
So, we are define a constructor for Animal and use it, go back to our code Animal.cs:
 ```diff
 using System.Windows.Forms;
namespace Northwind.Training
{
    class Animal
    {
       public void Run()
       {
           public string Name;
           public string AnimalType;
+          public Animal()
+          {
+               Name = "No name was given";
+               AnimalType = "No type was given";
+          }
           public void DescribeYourSelf()
           {
            MessageBox.Show(this.Name+" is a "+this.AnimalType); 
           }  
       }     
    }
}
```
In the constructor we can set also the default for this class, so if we define a new member `c` like :

```diff
using System.Windows.Forms;
namespace Northwind.Training
{
    class ClassesAndInstances
    {
       public void Run() 
       {
            Animal a = new Animal();
            Animal b = new Animal();
            a.Name = "Rex";
            b.AnimalType = "Dog" ;
            b.Name = "Kitty";
            b.AnimalType = "Cat" ;
            a.DescribeYourSelf();
            b.DescribeYourSelf();
+           Animal c = new Animal();
+           c.DescribeYourSelf();
       }     
    }
}
```
As we don't define c.Name and c.AnimalType, it get the default with the method Animal(). Build it and run
```diff
using System.Windows.Forms;
namespace Northwind.Training
{
    class ClassesAndInstances
    {
       public void Run() 
       {
            Animal a = new Animal();
            Animal b = new Animal();
            a.Name = "Rex";
            b.AnimalType = "Dog" ;
            b.Name = "Kitty";
            b.AnimalType = "Cat" ;
            a.DescribeYourSelf();
            b.DescribeYourSelf();
            Animal c = new Animal();
+           c.Name = "Snoopy";
+           c.AnimalType = "Dog" ;
            c.DescribeYourSelf();
       }     
    }
}
```
Build it and run it.
You can see that the default are overwritten by the setting that we set.

For our next test, we want that each animal has an unique identifier, so we change Animal.cs

 ```diff
 using System.Windows.Forms;
namespace Northwind.Training
{
    class Animal
    {
       public void Run()
       {
+          static int LastUsedId =0;
+          public int Id;            
           public string Name;
           public string AnimalType;
           public Animal()
           {
+               LastUsedId++;        
+               Id = LastUsedId;    
                Name = "No name was given";
                AnimalType = "No type was given";
           }
           public void DescribeYourSelf()
           {
-           MessageBox.Show(this.Name+" is a "+this.AnimalType); 
+           MessageBox.Show(this.Name+" is a "+this.AnimalType+ " and it's id is :"+ Id );
           }  
       }     
    }
}
```

After adding Id object, we need to store somewhere the last used Id it why we will use a static class

Note : some developers can make by mistake something like `c.Id = 9;` but we don't want allow that developer can change the Id. So the way to make variable unchangeable is to define that variable to `public readonly int Id`.
In this example, the value of the Id cannot be changed in the method, even though it is assigned a value in the class constructor.

<iframe width="560" height="315" src="https://www.youtube.com/embed/pyuGLDnGk2U?list=PL1DEQjXG2xnKI3TL-gsy91eXbh3ytOt6h" frameborder="0" allowfullscreen></iframe>