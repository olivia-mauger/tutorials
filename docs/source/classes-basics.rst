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

The first thing to note about the ``Otter`` class are its **member variables** (or **fields**)  as seen in **Lines 6-9**. Member variables, in essence, represent a class’s attributes. They "belong" to the class (i.e. in the scope of it).  For example, imagine you are looking at a real, live otter (lucky you!). How would you describe or define the animal? Does it have a name? Habitat? Mate? Age? All of these questions can be translated into specific **member variables** of the ``Otter`` class. ``name`` is a ``String`` variable, ``mate`` a ``boolean``, ``age`` an ``int``, and ``habitat`` a ``String`` as well. There is no limit to how many member variables a class can have, and there is no minimum requirement. In fact, a class does not *need* to have fields at all. 

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

Looking back at the ``Otter`` class, you can see in the constructor parameter list that it requires two ``String`` s and an ``int`` *in that order*. Thus, that is why we passed in "Olive", "River", and 2 when creating the object. 


**The Constructor Body**

Now that you know how to create an object, let’s examine how the body of the constructor works (**Lines 16-19**). **Overall, the goal of the constructor is to initialize the class’s fields, using the parameters passed in.** Thus, ``fieldName = paramName;`` is the order in which the statement should be written. Consider **Line 16**, ``name = n;`` In the example above, the first parameter of the ``Otter`` object ``olive`` was "Olive", so ``n`` holds this value. Since ``name = n;``, the field``name`` is now equal to "Olive”. 

What happens if the parameter name is the same as the field name? Although this is legal in Shadow, it can sometimes become confusing which variable is being referenced. Take a look at **Line 18**. Both the field and the parameter (which acts as a local variable) have the same name, ``age``. Although the code would still compile if you said ``age = age;``, it can become quite ambiguous which ``age`` is which. Thus, if you choose to name the field and the parameter the same, use the the ``this`` keyword. By saying ``this:age = age;``, the program knows the first 	``age`` is the field, or member variable. 

In addition, not all fields need to be initialized using parameter values like in **Line 19**.  The field ``mate`` is set to ``false``, as we are assuming an ``Otter`` object does not have a mate when it is first created. 

.. note:: We also could have set the field ``mate`` equal to ``false`` at **Line 8** where the variable was initially declared. 

Overloaded Constructors
^^^^^^^^^^^^^^^^^^^^^^^




