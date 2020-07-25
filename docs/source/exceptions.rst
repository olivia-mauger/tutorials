Exceptions
----------

Although we are officially covering **exceptions** now, you have most likely come across exceptions in earlier tutorials. In basic terms, an **exception** is like an official error message, an indication that something has gone wrong in a program. In other words, you have violated some Shadow "rule" or principle, and an exception is subsequently thrown.  

Common Exceptions 
^^^^^^^^^^^^^^^^^

Consider the following instance of an exception being thrown: 

.. code-block:: shadow 

    String[] nonsense = {"Chicken", "Pot", "Pie", "Yum"}; 
    Console.printLine(nonsense[4]); 
    Console.printLine("Continue?"); 

The console displays, in red text, 

.. code-block:: console

    shadow:standard@IndexOutOfBoundsException: Index 4

This console output is an example of an ``IndexOutOfBoundsException``, which belongs to the Shadow ``standard`` package (information before the ``@``).  An ``IndexOutOfBoundsException`` is thrown if you try to access a position in an array, ``String``, ``LinkedList``, or ``ArrayList`` that  does not exist. In this case, our ``String`` array, ``nonsense``, only has indices 0-3, so trying to print the value at index 4 results in this specific exception. We are referencing a position that is "out of bounds" of the array, and the exception message actually displays this index number. Once the exception is thrown, the program terminates, so "Continue?" will not be printed to the console. 

Although this exception is thrown automatically at run time, we are also able to explicitly throw exceptions ourselves. The syntax is as follows: 

``throw IndexOutOfBoundsException:create();`` 

This statement would produce the same output as the example above, excluding the ``Index 4``. 

Overall, an ``IndexOutOfBoundsException`` is just one exception in the Shadow ``standard`` package. Other exceptions and brief explanations from the Shadow API are below. 

* ``CastException`` (trying to cast one type to an incompatible type)
* ``Exception`` (parent type of all exceptions) 
* ``IllegalArgumentException`` (an argument with an illegal type or value is supplied to a method)
* ``InterfaceCreateException`` (trying to create an ``interface`` at run time) 
* ``NumberFormatException`` (parsing a ``String`` or other representation of a number and illegal characters are encountered)
* ``UnexpectedNullException`` (a ``nullable`` value is checked, found to be ``null``, and is not within a ``try`` block with a matching ``recover`` block) 

Writing and Catching Exceptions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Writing Exceptions** 

While we have covered "built-in" exceptions in Shadow, you are also able to create your own exceptions using the ``exception`` keyword. In order to understand **writing** and **catching** exceptions, consider the extended example outlined below: 

In the midst of a global pandemic, you realize that you have a lot of free time on your hands. Naturally, you decide to fill this time by learning how to cook. Although you have mastered mac ‘n cheese and toast, you are ready to move on to some more "advanced" recipes. Just in case, you decide to outline some things that could go wrong in the kitchen by defining 3 different **exceptions**. 

The first exception is called ``BurnedFoodException``: 

.. code-block:: shadow 
    :linenos: 

    exception tutorials:except@BurnedFoodException
    {
        public create()
        {
            super("Oh no! You have burned the food!");
        }
    }

The second is ``MeasuringMistakeException``: 

.. code-block:: shadow 
    :linenos: 

    exception tutorials:except@MeasuringMistakeException
    {
        public create()
        {
            super("Brush up on your fractions! You measured wrong!"); 
        }
    }

The last is ``OutOfIngredientsException``: 


.. code-block:: shadow 
    :linenos: 
    
    exception tutorials:exceptOutOfIngredientsException
    {
        public create()
        {
            super("Whoops! You ran out of ingredients!"); 
        }
    }


Upon examining these 3 different ``Exception`` classes, there are a few key things to take away. For one, instead of the keyword ``class``, they are all created with the following syntax: ``exception ClassName``. 

In addition, each has a single constructor that calls the parent class’ constructor via ``super()``. As for all exceptions, the parent class is called ``Exception``. ``Exception`` has 2 constructors, one that takes no parameters (creating an ``Exception`` without a message) and one that takes a ``String`` representing an explanation for the exception. In all three examples, we have invoked the parent constructor that takes in a ``String``. These ``String`` values are the messages displayed when the specific exception is thrown. For instance, if in a driver class we stated, ``throw MeasuringMistakeException:create();``, the console output would have been ``except@MeasuringMistakeException: Brush up on your fractions! You measured wrong!``

Now that we have established **how** to create our own exceptions, it is time to move on to **catching exceptions**. 

**Catching Exceptions**

Although knowing how to create and throw exceptions is important, it is even more useful to know how to **catch** them. As you have seen from the previous examples, when an exception is thrown, the program stops running at that point. **Catching** an exception circumvents this issue by identifying and "preventing" the exception that may or may not result when a given action is taken. 

Let’s revisit our cooking example by looking at the driver program, ``ExceptionTest`` below. 

.. code-block:: shadow 
    :linenos: 

    import shadow:io@Console;

    class tutorials:except@ExceptionTest   
    {
        public main( String[] args ) => ()
        {
            try
            {
                runOut();  
            } 
	    catch (BurnedFoodException ex) 
	    {
	        Console.printLine("Warning: Turn down the heat on the stove!"); 
	    }
	    catch (OutOfIngredientsException ex)
	    {
	        Console.printLine("Warning: Make a trip to the grocery store!"); 
	    }
	    catch (MeasuringMistakeException ex)
	    {
	        Console.printLine("Warning: Double check your math"); 
	    }
        }         
	
        public burnFood() => ()
	{
	    throw BurnedFoodException:create(); 
	}
	
	public runOut() => ()
	{
	    throw OutOfIngredientsException:create(); 
	}
	
	public measureMistake() => ()
	{
	    throw MeasuringMistakeException:create(); 
	}
    } 

First, ignore the ``main()`` method and look at **Lines 25-39**. Here we see 3 methods: ``burnFood()``, ``runOut()``, and ``measureMistake()``. These methods represent 3 different actions you could take to ruin your cooking, so it makes sense that each of these methods throws a corresponding exception (defined above). If you simply called ``burnFood()`` in the ``main()`` method, you would get an exception with the message "Oh no! You have burned the food!", and the program would terminate. This is not very useful, especially if you want the program to keep running.

Wouldn’t it be better if you got a warning that you were about to burn your food or run out of ingredients? This is where the **try-catch** block comes in. The syntax is as follows: 

.. code-block:: shadow

    try
    {
        //some action
    }
    catch (Exception ex)
    {
        //action to take
    }

    .
    .
    .

There are no restrictions on the number or type of statements we can put inside the ``try`` block. We can call methods, create variables, create objects, etc. Look at **Line 9** of ``ExceptionTest``. Inside the ``try`` block, we are calling the method ``runOut()``, which throws an ``OutOfIngredientsException``. Once this exception is thrown, we say that it is **in flight**. In other words, the program goes back to the try-catch block and runs through each ``catch`` statement (from top to bottom) until it finds an exception of compatible type. 

In this example, the first ``catch`` block has the type ``BurnedFoodException``, so then the second ``catch`` block is checked. It is of type ``OutOfIngredients``, which matches the type of exception thrown by ``runOut()``. Subsequently, the program enters this ``catch`` block and executes all statements inside of it. Thus, "Warning: Make a trip to the grocery store!" is printed to the console. Then, the try-catch block is exited completely and any statements after the ``runOut()`` method call will **not** execute. Control then flows to the first statement outside of the try-catch block. 

Overall, by using a try-catch block, we were able to handle the ``OutOfIngredients`` exception ourselves, as opposed to letting the exception simply be thrown by the program. That is, instead of "running out of ingredients" (i.e. getting the exception error message), you got a "warning" instead. 


More on Catching Exceptions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Although we have covered the basics of creating a try-catch block in the previous example, there are some important nuances and rules that are outlined below. 

* There is no limit to how many ``catch`` blocks you can have 
* If you do include **multiple** ``catch`` **blocks**, the **most specific** exceptions should be put first, getting more general/broad at the end. For example, let’s say we added the ``catch`` statement -- ``catch (Exception ex)`` -- as the first ``catch`` after the ``try`` block. Since all exceptions are children of ``Exception``, any exception that could be thrown would match with this first ``catch`` block. Thus, none of the other ``catch`` blocks could ever be reached, **leading to a compile error** ( ``Unreachable code:`` ). 
* If an exception is thrown from a ``try`` block and is never caught, the program simply terminates and the exception is displayed on the console. 










    

