
----------------------
Variables Introduction
----------------------

One key concept common for almost every programming language is called a variable. Just like in mathematics where you might say 3x = 24 (where x is the variable equal to 8), variables in Shadow hold values. However, unlike in mathematics (where variables have fixed and sometimes unknown values), Shadow uses **imperative assignment**. This means that when a variable is **assigned**, its value (or reference) changes. 

Numeric Types
^^^^^^^^^^^^^

Key **numeric type** variables, which are examples of **primitive variables** and store **literal values**, are listed with their sizes and ranges below:

+----------------------------+------------------------+----------------------------+-------------------+
|                                            Signed Types                                              |
+=========+==================+========================+============================+===================+
| **Type**|**Size (Bytes)**  |    **Minimum Value**   |   **Maximum Value**        |**Example Literal**|
+---------+------------------+------------------------+----------------------------+-------------------+
| ``byte``|     1            |          -128          |         127                |       ``64y``     |
+---------+------------------+------------------------+----------------------------+-------------------+
|``short``|     2            |         -32768         |        32767               |      ``1000s``    |
+---------+------------------+------------------------+----------------------------+-------------------+ 
| ``int`` |     4            |      -2147483648       |      2147483647            |       ``15``      |
+---------+------------------+------------------------+----------------------------+-------------------+       
| ``long``|     8            |  -9223372036854775808  |  9223372036854775807       |       ``0L``      |
+---------+------------------+------------------------+----------------------------+-------------------+


In addition to the above integer-like types, Shadow also has two types of primitive variables for storing **floating-point values** (i.e. 10.4 or 12.3564): ``double`` and ``float.``

Unlike Java, Shadow has **unsigned types** for primitive variables as well. For example, an unsigned ``int`` is represented as ``uint``. However, casting is still needed if you want to store an uint in an int, or vice versa. Due to strict Shadow type-checking, exercise caution when using unsigned variables.

.. note:: There is no ``udouble`` or ``ufloat`` class!


+-----------------------------+------------------------+-------------------------+
|                               Unsigned Types                                   |
+==========+==================+========================+=========================+
| **Type** |**Size (Bytes)**  |  **Maximum Value**     |**Example Literal**      |
+----------+------------------+------------------------+-------------------------+
|``ubyte`` |     1            |          255           |         ``128uy``       |      
+----------+------------------+------------------------+-------------------------+
|``ushort``|     2            |         65535          |         ``1000us``      |      
+----------+------------------+------------------------+-------------------------+
| ``uint`` |     4            |      4294967295        |          ``15u``        |    
+----------+------------------+------------------------+-------------------------+    
| ``ulong``|     8            |  18446744073709551615  |          ``0uL``        |
+----------+------------------+------------------------+-------------------------+


As an example, a basic variable declaration of type ``int`` looks like this: 

.. code-block:: shadow

    int age = 20; 

The **variable** ``age`` is of **primitive** type ``int`` and holds the **literal value** ``20``.

Boolean
^^^^^^^

There is one other primitive type: ``boolean``.  A boolean variable can hold one of two values -- ``true`` or ``false``. 

For example, 

.. code-block:: shadow

    boolean isBeautiful = true; 

The **variable** ``isBeautiful`` is of **primitive** type ``boolean`` and holds the value ``true``. 

Strings and Immutability
^^^^^^^^^^^^^^^^^^^^^^^^^

Although Strings will be discussed more in-depth in a later tutorial, the basics are outlined here. 

While it appears that a Shadow variable can be declared of type ``String``, you are actually creating an object of the ``String`` class (see “Shadow Classes”). This means that unlike a numeric variable which holds a literal value (like the number 20), ``String`` variables hold **references** (a location in memory) to an object. 

For example, 

Let’s use our ``age`` variable again (``int age = 20;``). If you had a birthday and wanted to update your age, you could write the following line of code: 

.. code-block:: shadow

    age = 21; 

Now the variable ``age`` is updated and holds the literal value of 21. Notice how I did not write 

.. code-block:: shadow

    int age = 21; 

This code would not compile because the ``age`` variable is already declared and **cannot be declared twice**. You are not trying to create a whole new ``age`` variable; you are simply changing its value. 

However, now consider the following ``String`` variable. 

.. code-block:: shadow

    String name = "Olivia"; // note: you must put the characters in quotes

Let’s say you wanted to change your name to "Stephanie" :

.. code-block:: shadow 

    name = "Stephanie"; 

While this statement is legal and would compile, it is important to note that you are not changing the literal value of the ``name`` variable. Because Strings hold references to an object, you are actually creating a new reference to a new object that the variable name now points to. Thus, we say that Strings are **immutable**.  

Code Example and Variable Names
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following short example program demonstrates basic principles for declaring and assigning variables, as well as some information on formatting output for ``Console.printLine()``.


.. code-block:: shadow
 
    import shadow:io@Console;  

    /*This is a short bit of code the demonstrates how to the declare the variable 
    types defined above. */

    class VariableExample
    {
	public main( String[] args ) => () 
	{	
		String restaurantName = "Taco Tuesday"; 
		boolean isHungry = true; 
	
		String meal = "Meat and Bean Burrito"; 
		int quantity = 2; 
		double price = 5.50; 
		
		Console.printLine("I love eating at " # restaurantName # "."); 
		Console.printLine("I would like " # quantity # " " # meal # "(s).");  
	}
	
    }

The output is as follows: 

.. code-block:: console

    I love eating at Taco Tuesday.
    I would like 2 Meat and Bean Burrito(s).


To analyze this code, let's break it up into sections. 

1) **CamelCase Notation**

.. code-block:: shadow

    String restaurantName = "Taco Tuesday"; 
    boolean isHungry = true; 

The most important thing to note here is how the variables are named. For example, ``restaurantName`` is a ``String`` variable. Notice how I did not name it ``RestaurantName`` or ``restaurantname``. Although using these names would not cause a compile error, it is good programming practice to use **CamelCase** notation: where the first word in a sequence of words (that are not separated by spaces) begins with a lowercase letter and the rest begin with uppercase letters. The same goes for the ``boolean`` variable ``isHungry``. In addition to using CamelCase notation, it is also a good idea to make sure your variable names are descriptive of their purpose. In this case, if this was a program for a Restaurant, ``isHungry`` would be used to tell if a certain customer is hungry -- as can be inferred from the variable's name. 
  
.. note:: Your code will not compile if you have spaces in variable names, i.e. ``restaurant name``
 
2) **More Naming Conventions**

.. code-block:: shadow

    String meal = "Meat and Bean Burrito"; 
    int quantity = 2; 
    double price = 5.50; 


There are a few more key naming conventions for Shadow. 

    * Starting a variable name with a number will cause a compile error (but ending it with a number is acceptable) 
    * Single-word names should be all lowercase (i.e. price, meal, or quantity), but is not a compile error 
    * Starting a variable name with a special symbol (i.e. #, _, @, % +, etc.) will cause a compile error 
    * Variable names cannot be **reserved words** (see next section). 


3) **Formating Output** 

.. code-block:: shadow 

    Console.printLine("I love eating at " # restaurantName # "."); 
    Console.printLine("I would like " # quantity # " " # meal # "(s).");
    
As explained in a previous section "Printing text", ``Console.printLine()`` is used to display text on the console. Literal text goes in " ", but you are also able to print variable values as well. For example, as seen in the above segment of code, say you want to output ``I love eating at Taco Tuesday.`` You could easily just type out "Taco Tuesday" in between the " ". However, you could also use the variable ``restaurantName`` and print its literal value, which is also "Taco Tuesday". To do so, use the **octothorpe** (``#``) on either side of the variable’s name outside of the " " (see above).  Thus, in place of ``# restaurantName #``, ``Taco Tuesday`` will be printed. 

Since these two methods result in the same output, what is the advantage of using the ``#``? Let’s say in the line after you declare ``restaurantName`` you decide you want to eat at a different restaurant and write 

.. code-block:: shadow

    restaurantName = "Taco Wednesday"; 

If you still wanted to use ``Console.printLine("I love eating at " # restaurantName # ".");`` to output ``I love eating at Taco Wednesday``, now you do not have to change any code because ``# restaurantName #`` will retrieve the most "recent" value for restaurantName.  


Reserved Words
^^^^^^^^^^^^^^

In Shadow, and with most programming languages, there are **reserved words.** Reserved words inherently have meaning in Shadow. For example, ``double`` is a **reserved word** because Shadow recognizes this as a primitive type -- it has meaning. *Thus, you will get a compile error if you try to name a variable with a reserved word.* See the chart below for a full list of reserved words in Shadow. 


============  ==============  ============  =============  =============  =============  =============  
``abstract``   ``and``        ``assert``    ``boolean``    ``break``      ``byte``       ``case`` 
``cast``       ``catch``      ``check``     ``class``      ``code``       ``constant``   ``continue``
``copy``       ``create``     ``default``   ``destroy``     ``do``        ``double``     ``else``
``enum``       ``exception``  ``extern``    ``false``      ``finally``    ``float``      ``for``  
``foreach``    ``freeze``     ``get``       ``if``         ``immutable``  ``import``     ``in``
``int``        ``interface``  ``is``        ``locked``     ``long``       ``native``     ``null`` 
``nullable``   ``or``         ``private``   ``protected``  ``public``     ``readonly``   ``recover``
``return``     ``send``       ``set``       ``short``      ``singleton``  ``skip``       ``spawn``
``super``      ``switch``     ``this``      ``throw``      ``true``       ``try``        ``ubyte``
``unit``       ``ulong``      ``ushort``    ``var``        ``weak``       ``while``      ``xor``
============  ==============  ============  =============  =============  =============  =============  







 












 
