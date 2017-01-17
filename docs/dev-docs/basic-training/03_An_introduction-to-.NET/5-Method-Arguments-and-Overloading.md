﻿### Method Arguments and Overloading
Method arguments are sent between brackets.

To see the arguments the method receives you can:
1. Type open parenthesis 
2. Click the method parameter button on the toolbox when the cursor is between the parenthesis:

![Show Arguments](../Visual-Studio-Configuration/Show-Arguments.png)

3. Press **Ctrl+Shift+Space** when the cursor is between the parentheses.


**Overloading** allows Methods to have the same name but with different combination of parameters.
![Method Overloading](Method_Overloading.png)
 
Method can have several options based on the number or type of parameters it receives.

Based on the parameters sent the matches method is be called.

For example the Show() method of System.Window.Forms.MessageBox class can receive the text to be displayed on the message box as parameter.
It can also receive the Text and the caption.
The Show() method has 21 overloads meaning it has 21 variant of the method that receive different combination of parameters.




```diff
namespace Northwind.Training
{
    Class HelloWorld
    {
       public void Run()
       {
-           System.Windows.Forms.MessageBox.Show("Hello World");
+           System.Windows.Forms.MessageBox.Show("Hello World", "Hello World Caption", System.Windows.Forms.MessageBoxButton.OK);
       }     
    }
}
```

 <iframe width="560" height="315" src="https://www.youtube.com/embed/Z97ayKhfYtE" frameborder="0" allowfullscreen></iframe>
