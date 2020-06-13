Flow Control and Looping
------------------------
So far, we have learned how to create a basic program in **Shadow**, declare and use variables, and write expressions with different kinds of operators. In the simple example programs we have analyzed thus far, it is easy to see how **control flows**. Execution starts with the first statement in the program (a variable declaration, ``Console.printLine()``, etc.) and continues to the second and third and so on. Nothing is skipped and no action repeated. Straightforward. 

However, **control flow** becomes more interesting as we begin to introduce new statements: ``if``, ``else``, ``break``, ``continue``, ``switch``, and different kinds of loops. These statements have the power to manipulate/direct the flow of a program, thus opening the door for more powerful programs. 


``if`` and ``else`` Statements
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Although ``if`` statements were briefly mentioned in a previous section ("Logical Operators"), they will now be covered in-depth. 

Below is the basic structure for an ``if``/``else`` statement. 


.. code-block:: shadow 

    if( ) //some expression that evaluates to true or false 
    { 
        //do something here 
    }
    else
    {
        //do something different here
    }

There are a few things to note: 

* You cannot have an ``else`` statement without a matching ``if`` statement, but you can have an ``if`` statement without an ``else``. 
* You cannot have multiple ``else`` statements with the same ``if`` statement. 
* The expression inside the ``if`` statement must evaluate to either ``true`` or ``false``. For example, you could NOT say ``if(int x = 6)``. This would cause a compile error. 
* Logical operators (and the others) are useful when writing ``if``/``else`` statements. 

**Nested** ``if``/``else`` **Statements** 

Another important concept is nested ``if``/``else`` statements. There are many different ways to structure these, and it is very important to be mindful of your use of ``{ }`` in order to control which ``if`` matches with which ``else``.  ``else`` statements match with the **closest** ``if`` statement, so lack of attention to brace placement can lead to some unintended outputs. For example, you may have an ``if``/``else``  enclosed inside of one larger ``if``, or you may choose to have sequences of ``else if`` statements. 

Below are some possible examples: 

.. code-block:: shadow  

    //Here is a example of a nested if/else statement (inside a larger if)
    var numDonuts = 4; 
    if(numDonuts > 0)
    { 
        //pay attention to how the use of brackets directs program flow
	if (numDonuts % 2 == 0)
	{
	    Console.printLine("You have an even number of donuts left!"); 
	    Console.printLine("Now you have to share."); 
	}
	else 
	{
	    Console.printLine("You have an odd number of donuts left !"); 
	}
			
    } //Notice how there is no else statement for the outside if. This is OK. 


The console output: 


.. code-block:: console 

    You have an even number of donuts left!
    Now you have to share. 


Lastly, here is an example of ``else if`` 


.. code-block:: shadow
    :linenos:

    /*
     *For his 25th Birthday, Surya and his friends decide to go to an amusement
     *park with 3 rides. Surya has never been to an amusement park before, so it is your 
     *job to determine which ride Surya would enjoy based off of his list of 
     * attributes. Good luck!
     */
		 
    var name = "Surya";  
    var scaredOfHeights = false; 
    var noLoops = true; 
    var idealRideSpeed = 100; 
		 
    if(scaredOfHeights and noLoops) 
    {
        Console.printLine("Sorry, there aren't any rides without loops or heights."); 
    }
    else if(!scaredOfHeights and idealRideSpeed >= 110) 
    {
        Console.printLine("You would love the Super Speedy Plunge!"); 
    } 
    else if(!noLoops or idealRideSpeed < 80) 
    {
        Console.printLine("Get in line for the Loop Dee Loop"); 
    }
    else
    {
        Console.printLine("Get ready to go on Madness Mountain!"); 
    }


Which ride should Surya go on? 

.. code-block:: console

    Get ready to go on Madness Mountain!


Why should Surya go on Madness Mountain? Let's trace through the code. 

Lines 8-11 establish the "rules" for determining what ride he should go on. We know that he prefers rides that go 100 mph, don’t have loops, and have heights. Control then is passed to  **Line 13**. This expression evaluates to ``false`` because ``scaredOfHeights`` is ``false``. This means that the statement inside the first ``if`` is skipped, and execution is passed to **Line 17**. Since his ideal ride speed is not greater than or equal to 110 mph, the expression evaluates to ``false`` and control is passed to **Line 21.** Neither statement is ``true``, so the last ``else if`` evaluates to ``false``. Therefore, the statement inside the final ``else`` is printed (there is no condition) and Surya should ride Madness Mountain. 

It is important to note that if one of the earlier ``else if`` statements had evaluated to ``true``, the rest of the ``else if`` and final ``else`` would NOT be evaluated, and control would be passed to the the next line after the final ``else``. 


**One Final Note** 

Technically, if an ``if`` statement is followed by a single line of code, braces are not needed. However, it is good programming practice to *always* do so, as it can lead to some unintended output. See below: 


.. code-block:: shadow

    if(1 > 2)
        Console.printLine("hey"); 
        Console.printLine("hi"); 

Since both statements following the ``if`` are indented, you might assume that both "hey" and "hi" will NOT be printed. However, even though 1 is certainly not greater than 2, "hi" is still printed because when braces are not present, only the first line after the ``if`` is considered part of it. 


``while`` Loops 
^^^^^^^^^^^^^^^

Now, we will shift to **loops**, specifically ``while`` loops. But first, we must answer a basic question: *What is a loop?* As with Shadow, and programming in general, sometimes you will need to repeat an action multiple times. For example, let's say for some random reason I wanted to write a program that outputs "I love Shadow!" 5 times in a row. I could easily write ``Console.printLine("I love Shadow!")`` 5 separate times. However, this can become quite tedious and inefficient. Cue **loops**.  Loops allow you to repeat code for a specified number of times, or while a certain condition is met. 

The first type of loop discussed is ``while`` loops, which repeat code based off of some boolean expression. The basic structure is below: 


.. code-block:: shadow

    while () //boolean expression
    {
        //block of code to repeat
    }


Although not defined above, a key concept for ``while`` loops, and really any loop, is the **control variable or loop counter**. This variable controls how many times the loop will execute and prevents **infinite looping**. 

For example, let’s examine this block of code: 


.. code-block:: shadow

    var favoriteNumber = 13; 
    while (favoriteNumber > 0)
    {
        Console.printLine("Your favorite number is " # favoriteNumber); 
    }

What happens? This is a basic example of an **infinite loop**. The ``boolean`` expression ``favoriteNumber > 0`` will always evaluate to ``true``, so "Your favorite number is 13" will be printed an infinite number a times, causing the program to crash. There is, however, a way to prevent this by using a **loop counter.**





		
