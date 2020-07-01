Classes: The Basics
-------------------

Congratulations! Now that you have reached this point in the tutorials, you should have good understanding of the basics of the  **Shadow** language. We have covered everything from variables, operators, and methods to arrays and loops. Now, it is time to move on to classes, objects, and interfaces — three crucial topics. Similar to Java, **Shadow** is part **Object-Oriented**. However, before we dive into creating and using objects, we must first define the key components of a **Shadow** class. 

Whenever we write a program, we always start by creating and naming the class that serves as the "container" for our code. So far, we have been writing the majority of our code directly inside the ``main()`` method to test out the language basics. However, this is not entirely realistic. In most cases we we want to define a **class** that represents some **object**, or idea. Then, we create and test the methods/properties of objects of the class in the ``main()`` method. 

In order to explain the concepts behind classes and objects, we will be analyzing an extended example of the ``Otter`` class. In a literal sense, otters are objects, and we can create class a that represents them. Read through the program below to get familiar with it before we break it down. 


.. code-block:: shadow 
    :linenos:   

    class Otter
    {
        /* These are the private member variables
	 * of the Otter class.
	 */
	get String name; 
	get set String habitat; 
	get set boolean mate; 
	get set int age; 
	
	/* This is the contructor for the Otter class,
	 * which initializes its private memebers.
	 */
	public create(String n, String h, int age) 
	{
	    name = n; 
	    habitat = h; 
	    this:age = age; 
	    mate = false; 
	} 
	
	/* Implementation of the set method
	 * for the member variable mate. 
	 */
	public set mate(boolean value) => ()
	{
	    if( value and age > 2 )
	    {
	        mate = true;
	    }
	}

	/*This is a method that is part of 
	 * the Otter Class. It returns an int 
	 * representing the number of fish caught. 
	 */
	public goFishing() => (int)
	{
	    int numFish; 
	    if ( mate ) 
	    {
	        numFish = 10; 	
	    }
	    else 
	    {
	        numFish = 5; 
	    }
			
	    return numFish; 
	}	
    }

Member Variables
^^^^^^^^^^^^^^^^

The first thing to note about the ``Otter`` class are its **member variables** (or **fields**)  as seen in **Lines 6-9**. Member variables, in essence, represent a class’s attributes. They "belong" to the class (i.e. in the scope of it).  For example, imagine you are looking at a real, live otter (lucky you!). How would you describe or define the animal? Does it have a name? Habitat? Mate? Age? All of these questions can be translated into specific **member variables** of the ``Otter`` class. ``name`` is a ``String`` variable, ``mate`` a ``boolean``, ``age`` an ``int``, and ``habitat`` a ``String`` as well. There is no limit to how many member variables a class can have, and there is no minimum requirement. In fact, a class does not *need* to have member variables at all. 

Aside from the words ``get`` and ``set``, declaring a member variable is the same as declaring any local variable. The difference, though, is that every member variable is automatically declared ``private``. You do need to and should not include this **reserved word** as a modifier. It is a given. When ``private`` is used to modify a variable, it means that the variable can only be accessed **within the class that it is declared in**. This is exactly why we use ``get`` and ``set``: to allow other classes to be able to access or change the value of these private member variables. ``get`` and ``set`` will be explained in the later section, "Accessing Member Variables". 

**A Brief Conceptual Note** 

It is important to understand that the ``Otter`` class *is not an otter object*. Rather, it is like a framework or blueprint that describes the attributes, features, and "actions” of an otter in general. The member variables **do not** need to be (but they can be) initialized to a literal value (i.e. every otter will probably not live in the same place or have the same age). Rather, when we create an object, or an **instance** of the otter class (usually in the ``main()`` method), we send in literal values as parameters, which  initialize the member variables to these user-defined values. You may be asking, how do we create an object, and how are these values are initialized? The next section will cover this in detail. 


Constructors and Objects Intro
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A **constructor** is another key element in a Shadow class and can be seen in **Lines 14-20** of the example program. Syntactically almost the same as a method, **constructors** are how the instances of a class (or objects) are created. The general method header for a constructor is as follows: 

``public create(parameters passed in)``

No matter the name of the class, a constructor must always start with ``public create``. The number and type of parameters will vary by class. Before we get into the body of the constructor, let’s go over the basic syntax of creating an object in Shadow, which will probably remind you of how arrays are declared. 

**Creating an Object**

As aforementioned, objects are typically created in the ``main()`` method of a class. Although we could have a ``main()`` method in the ``Otter`` class itself, it is also common to create a separate **driver** class where the functionality of a class can be tested. For example, say we have another class called ``OtterDriver`` with a ``main()`` method. 

.. note:: The driver class should be placed in the same directory/folder as the class you are testing. 

The first line of the ``main()`` method is: 

``Otter olive = Otter:create("Olive", "River", 2);``

``Otter olive`` is how we declare the object. The type, which has to be the **name of the class** , is ``Otter``. ``olive`` is the name of our object, or an instance of the ``Otter`` class. The same naming conventions outlined in "Variables Introduction" should be followed. There is no limit on the number of ``Otter`` objects we can create. 

The expression to the right of the equals sign invokes the object’s **constructor** and thus creates an ``Otter`` object (as made clear by the reserved word ``create``). Inside the parentheses we see 3 literal values. Much like the method calls discussed in an earlier tutorial, **constructors** can take in parameters. 

Looking back at the ``Otter`` class, you can see in the constructor parameter list that it requires two ``String``variables and an ``int`` *in that order*. Thus, that is why we passed in "Olive", "River", and 2 when creating the object. 


**The Constructor Body**

Now that you know how to create an object, let’s examine how the body of the constructor works (**Lines 16-19**). **Overall, the goal of the constructor is to initialize the class’s member variables, using the parameters passed in.** Thus, ``fieldName = paramName;`` is the order in which the statement should be written. Consider **Line 16**, ``name = n;`` In the example above, the first parameter of the ``Otter`` object ``olive`` was "Olive", so ``n`` holds this value. Since ``name = n;``, the member variable ``name`` is now equal to "Olive". 

What happens if the parameter name is the same as the member variable name? Although this is legal in Shadow, it can sometimes become confusing which variable is being referenced. Take a look at **Line 18**. Both the member variable and the parameter (which acts as a local variable) have the same name, ``age``. Although the code would still compile if you said ``age = age;``, it can become quite ambiguous which ``age`` is which. Thus, if you choose to name the member variable and the parameter the same, use the ``this`` keyword. By saying ``this:age = age;``, the program knows the first ``age`` is the field, or member variable. 

In addition, not all member variables need to be initialized using parameter values like in **Line 19**.  The member variable ``mate`` is set to ``false``, as we are assuming an ``Otter`` object does not have a mate when it is first created. 

.. note:: We also could have set the field ``mate`` equal to ``false`` at **Line 8** where the variable was initially declared 

Overloaded Constructors
^^^^^^^^^^^^^^^^^^^^^^^

Just like **methods** in Shadow, constructors can also be **overloaded**. This simply means that each overloaded constructor’s parameter list must vary in type and/or number than the others. For example, if one constructor took in a ``String``, an overloaded constructor could take in more than one ``String``, a ``String`` and a ``code``, etc. 

Consider this additional constructor for the ``Otter`` class: 


.. code-block:: shadow 
    :linenos:  

    public create(String n, String h) 
    {
        name = n; 
	habitat = h; 
	age = 0; 
	mate = false; 
    }


The only difference is this overloaded constructor does not take in an ``int`` representing age. It sets the member variable ``age`` to 0 when the object is created. 

Thus, the following statement is now valid: 

``Otter oliver = Otter:create("Oliver", "Ocean");``

The program recognizes that this second constructor exists, and now ``oliver`` has ``age = 0;``. It is important to recognize that both ``olive`` and ``oliver`` are still otters. They were just created invoking different constructors. 

Default Constructors
^^^^^^^^^^^^^^^^^^^^
What happens if a constructor is not explicitly defined by the programmer? Can you still create an object of the class? The answer is **yes**. 

When no constructor is present, **Shadow** invokes a **default constructor**, where member variables are given default values. ``int`` would be 0, ``double`` 0.0, ``boolean`` ``false``, and ``code`` '\0'. However, what happens to a ``String`` member variable? Unless it is declared to be **nullable**, you will get a compile error that says: 
``Uninitialized field: Non-nullable field name might not be initialized by a create``

Marking a ``String`` member variable as ``nullable`` allows the variable to hold the value ``null``, and thus, the default constructor to be invoked. You should also declare a ``String`` array to be ``nullable`` if it is a member variable and you are invoking the default constructor. ``nullable`` will be covered more in-depth in a later section. 

Lastly, if you have at least one programmer-defined constructor, you will get a compile error if you try to invoke the default constructor. 

``get`` and ``set`` Properties
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We are now going to move back to our analysis of the ``Otter`` class and address the properties ``get`` and ``set``. 

Because all member variables (or fields) in Shadow are ``private``, how can other classes access or change these values? It would be quite tedious to write **accessors** (a method that returns the value of a member variable)  and **mutators** (a method that updates/changes the value of a member variable) for each field. Instead, we use **properties**. Properties are accessed with the arrow operator (``->``). 

In order to see how properties work, take a look at **Line 6** of the ``Otter`` class: 

``get String name;``

Here ``get`` the property is modifying the member variable ``name``. We can then use this property in our ``OtterDriver`` program, part of which is shown below.


.. code-block:: shadow 
    :linenos: 

    Otter olive = Otter:create("Olive", "River", 6); 
    Console.printLine(olive->name # " lives in a " # olive->habitat); 
		
    olive->mate = true; 
    Console.printLine(olive->name # " found a mate! " # olive->mate); 
    Console.printLine(olive->name # " just caught " # olive.goFishing() # " fish!"); 
		
The program output is below: 

.. code-block:: console 

    Olive lives in a River
    Olive found a mate! true
    Olive just caught 10 fish!


In **Line 2** of the driver program we see ``olive->name``, which returns the value of the member variable ``name`` ("Olive"), as shown in the console output. The same applies for ``olive->habitat``. If either ``name`` or ``habitat`` hadn’t had ``get`` in their declaration, you would’ve needed to write accessor methods for both in order to "get" their values in ``OtterDriver``. 

Additionally, ``set`` can be used to store a value into a member variable.  **Line 4** states ``olive->mate = true;``. If no ``set`` mutator method was defined in the program, the member variable ``mate`` would simply have been changed to ``true``. However, in the ``Otter`` class, a condition must be met before ``mate`` is set to a new value (code excerpted below): 

.. code-block:: shadow 
    :linenos: 

    public set mate(boolean value) => ()
    {
        if( value and age > 2 )
	{
	    mate = true;
	}
    }

In order for the property to work correctly, the method header is critical. The syntax is as follows:  

``public set memberName(var of member type) => ()``

In the ``Otter`` class, the member variable name is ``mate`` and the type is ``boolean``, as reflected in the method header. Now, ``mate`` will only be set to ``true`` if the ``Otter`` object has an age greater than 2. As you can see in the console output from ``OtterDriver``, ``olive`` is ``6``, so she has found a ``mate``! 

.. note:: This method and indeed all properties can also be called directly as methods (since that's what they are, under the covers), but we suggest that property syntax is used whenever possible.


Class Methods
^^^^^^^^^^^^^

Outside of  **constructor(s)**, **accessors**, or **mutators**, classes can have any 
number of other methods, as discussed in the previous "Methods" tutorials. If you need a refresher on how to create, use, or call methods, refer back to this section. 

Notice how the ``Otter`` class has a method called ``goFishing()`` (see below) 


.. code-block:: shadow 
    :linenos: 
    
    public goFishing() => (int)
    {
        int numFish; 
	if ( mate ) 
	{
	    numFish = 10; 	
	}
	else 
	{
	    numFish = 5; 
	}
			
	return numFish; 
    }	


The method takes in no parameters and returns an ``int`` representing the number of fish caught. If the ``Otter`` object the method is called on has a mate, twice the number of fish are caught. As seen in **Line 6** of the ``OtterDriver`` class, all you need to do to call the method on an ``Otter`` object is to use the following syntax: 

``objectName.methodName(parameters);``

Defining different methods within a class gives the class greater functionality and makes objects even more useful. Now, we are ready to move on to more advanced topics regarding classes.  










    




