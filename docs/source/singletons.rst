Singletons
----------

In other programming languages, when a method or a variable is marked as ``static``, it means that the method or variable is shared between all instances of a class. It does not "belong" to an individual object. However, in **Shadow** ``static`` does not exist. Instead, we are able to create a specific type of class called ``singleton``. In a broad sense, defining a  ``singleton`` class means that **only one object of that class can exist at one time,** per thread. How does this work? Take a look at the example below. 

Example
^^^^^^^

Let's say I wanted to write a ``singelton`` class representing my birthday. See below. 

.. code-block:: shadow 
    :linenos: 

    singleton Birthday is CanOpenGifts
    {
        get set String month; 
	get int day; 
	get int year; 
	
        public create() 
	{
	    month = "November"; 
	    day = 28; 
	    year = 1999; 
	}
	
	public openGifts() => (String) 
	{
	    return "No more gifts to unwrap!"; 
	}

    }

Next, this is the interface that the ``singleton`` implements. 

.. code-block:: shadow 
    :linenos: 

    interface CanOpenGifts
    {
        openGifts() => (String); 
    }


The first thing to note is that ``singleton`` classes are able to implement interfaces in the same way as discussed in the previous tutorial. The syntax does not change. In addition, notice how in the ``singleton`` header the keyword ``class`` is omitted. You will get a compile error if you try to include it. 

However, the most important thing to take away is that **the constructor of a** ``singleton`` **class cannot take in any parameters**. **In fact, you do not even need to include a constructor for a** ``singleton`` class. You could simply declare and initialize the member variables at the same time. It would look like this: 


.. code-block:: shadow 
    :linenos: 
        
        get set String month = "November"; 
        get int day = 28;  
	get int year = 1999; 

.. note:: The properties ``get`` and ``set`` can be used for ``singelton`` classes 

Application
^^^^^^^^^^^

The following driver program demonstrates how a ``singleton`` object works: 

.. code-block:: shadow 
    :linenos: 

    import shadow:io@Console;

    class BirthdayDriver
    {
        public main( String[] args ) => ()
	{
	    Birthday celebrate; 
	    Birthday party; 
		
	    Console.printLine(celebrate->month); 
	    Console.printLine(party->month); 
		
	    celebrate->month = "December"; 
	    Console.printLine(party->month); 
		
	    Console.printLine(celebrate.openGifts()); 
	}
    }

The console output is: 

.. code-block:: console

    November
    November
    December
    No more gifts to unwrap!

Upon looking at **Lines 7 and 8**  it may seem like there are two different ``singleton`` objects for the ``Birthday`` class, which would be illegal. However, ``celebrate`` and ``party`` are **actually the same reference**. Look at **Lines 10 and 11**. Both ``get`` properties return the same value, "November". Additionally, when ``celebrate`` sets the ``month`` member variable to "December", this change is reflected in ``party`` as well (**Line 14**). 

It may also seem strange in **Lines 7 and 8** that the object does not appear to be initialized with the keyword ``create``. If you tried to write ``Birthday celebrate = Birthday:create();`` you would get a compile error. This makes sense. The whole point of a ``singleton`` is to have one object of the class at a time. The object’s creation is handled in the first method where it appears.

A note on ``Console``
^^^^^^^^^^^^^^^^^^^^^

The ``Console`` class is a great example of a ``singleton``.  The fact that only one ``Console`` object exists can be used as a shortcut for accepting user input and using ``Console.printLine()`` statements. See the example below: 

.. code-block:: shadow 
    :linenos: 

    Console out; // no create needed (or possible)
    out.printLine("Bring rap justice!");
    Console screen; // still the same object
    screen.printLine("Shut 'em down!");










