Properties of Classes
---------------------

Now that we have covered the basics of classes in **Shadow**, we can move on to some features/properties of classes. 

``immutable`` and ``freeze()``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In a previous tutorial under  "Variables Introduction", we discussed the concept of **immutability** in terms of a ``String``. When we say that a ``String`` is **immutable**, we mean that once it is created, **its value cannot be changed**. 

In **Shadow**, a ``String`` is not the only thing that is ``immutable`` -- classes and references can be as well. We will start with analyzing ``immutable`` classes. See the basic example below: 


.. code-block:: shadow 
    :linenos: 

    import shadow:io@Console;

    /* Imagine you own a restaurant, 
     * and you are looking to hire a 
     * another server. You use this 
     * class to create application 
     * objects. Once an object is  
     * created, which represents one
     * application, its contents can 
     * never change. Thus, we declare 
     * the class to be immutable.
     */

    immutable class JobApplication
    {
        get String name; 
        get int age; 
        get boolean experience; 
        get String skill; 

        public create(String n, int a, boolean e, String s) 
        {
            name = n;
            age = a; 
	    experience = e; 
	    skill = s; 
        }
	
        public evaluateApp() => () 
        {
            if ( age <= 18 or experience == false ) 
	    {
	        Console.printLine(name # " is not qualifed for the job!"); 
	    }
			
	    else 
	    {
	        Console.printLine(name # " would be a great employee!"); 
	    }	
        }
    }

In order to declare a class to be ``immutable``, the syntax is: ``immutable class ClassName`` (see **Line 14**).  The constructor and other methods within the class **cannot** be marked as ``immutable``, just the class header. 

Aside from the keyword ``immutable``, the ``JobApplication`` class does not *appear* to be any different from the other non-``immutable`` class we have studied, the ``Otter`` class. However, notice how none of the member variables are marked with the keyword ``set``. If you tried to do so, you would get a compile error because instances of ``immutable`` classes cannot be changed once they are created. Further, any method (outside of the constructor) that would try to change the contents of an object of an ``immutable`` class will result in a compile error. Yet, the method ``evaluateApp()`` is valid because although it uses the values of some member variables in an ``if`` / ``else`` , it does not attempt to change them. 

Syntax aside, why is it beneficial to create ``immutable`` classes, and why would we want to create ``immutable`` objects/references? The answer lies in the idea of **thread safety**. If  you have a program that is multi-threaded, it is possible that more than one thread could be trying to change a single object at the same time. This could lead to unintended results or errors in the program. Thus, by creating as many ``immutable`` objects as possible, you help to eliminate the chances of running into this problem. You can then pass around the object with confidence that it will not be changed. 
In order to understand how to create an immutable reference/object, take a look at the following driver program for the ``JobApplication`` class. 


.. code-block:: shadow 
    :linenos: 

    import shadow:io@Console;

    class ApplicationDriver
    {
        public main( String[] args ) => ()
	{
	    JobApplication chris = JobApplication:create("Chris", 20, true, "positive attitude"); 
	    chris.evaluateApp(); 	
	}
    }

The console output is: 

.. code-block:: console
    
    Chris would be a great employee! 

As you can see in the driver program, **when a class is declared to be** ``immutable``, you do not need to use the ``immutable`` keyword to make the object ``immutable``; it automatically is.  The ``evaluateApp()`` method is called and executes as expected.

However, let’s imagine that the ``JobApplication`` class is non- ``immutable``. How can we create an ``immutable`` instance of the class? **We use the** ``freeze()`` **method**. The ``freeze()`` method creates an ``immutable`` copy of the object it is called on. 

The syntax for using ``freeze()`` is below. 

``immutable JobApplication chris = freeze(JobApplication:create("Chris", 20, true, "positive attitude"));`` 

Using ``freeze()`` on the right side of the equals sign creates an ``immutable`` reference to a non- ``immutable`` object and stores it in the ``immutable`` object ``Chris``. If the statement on the left side of the equals sign had just been ``JobApplication chris``, then you would have gotten a compile error **because an** ``immutable`` **reference cannot be assigned to a non-** ``immutable`` **object (and vice versa).** 


``readonly``
^^^^^^^^^^^^

Although ``immutable`` references/classes can help with **thread safety**, the trouble is that an immutable reference cannot be stored into a normal reference without losing the guarantee that its contents are protected (as explained above). To mediate between the two different kinds of references, ``readonly`` references are used.

If a reference is marked as ``readonly``, it means that no mutable method can be called on it. However, it is useful because you can store either a normal reference or a ``immutable`` reference in it. Although this may not seem much different from an ``immutable``, with a ``readonly`` reference, someone might have a normal reference they can use to change the contents of the object. Conversely, with an ``immutable`` reference, it's as if all the references to the object are ``readonly``. No one can ever change the contents of such an object.

Although methods can be marked as ``readonly``, classes cannot be. In addition, all methods of an ``immutable`` class are ``readonly`` automatically. 


Arrays as Objects
^^^^^^^^^^^^^^^^^

``copy()``
^^^^^^^^^^^

``equal()`` 
^^^^^^^^^^^^

``destroy()`` 
^^^^^^^^^^^^^
