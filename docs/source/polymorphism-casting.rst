Polymorphism and Casting
------------------------

This brief, but very important, tutorial on **polymorphism** and **casting** touches on a key **Object-Oriented** programming principle. **Polymorphism**, an often confusing term to define, is best understood in terms of an example. Consider the classes from the :ref:`inheritance tutorial<Classes: Inheritance>`. There is a parent class called ``Employee`` and 3 child classes: ``Waiter``, ``Chef``, and ``Manager`` (only the ``Waiter`` implementation is shown, as ``Chef`` and ``Manager`` were given as exercises). All 3 of these child classes will inherit the methods ``clockIn()`` and ``clockOut()`` from ``Employee``. **Polymorphism** can be seen in their implementation. Let’s say we decided to override ``clockIn()`` in the child classes. Now, the "same " method calls on subclasses of ``Employee`` give completely different results. This is the essence of polymorphism: that these various objects (that share the same parent class) can take on many different behaviors. After all, polymorphism literally means "many forms". 

The following example will hopefully solidify your understanding of polymorphism, and lead us into casting. 

Example
^^^^^^^^

First, here is our parent class, ``SeaCreature``. 

.. code-block:: shadow 
    :linenos: 

    import shadow:io@Console;

    class tutorials:polymorph@SeaCreature
    {
        get String type; 
	get String ocean; 
	
	public create(String t, String o)
	{
	    type = t; 
	    ocean = o; 
	}
	
	public swim() => ()
	{
	    Console.printLine("This " # type # " is swimming!"); 
	}
    }

The following are two child classses of ``SeaCreature``. 


.. code-block:: shadow 
    :linenos: 

    import shadow:io@Console;

    class tutorials:polymorph@Dolphin is SeaCreature
    {
	public create(String t, String o)
	{
	    super(t,o); 
	}
	
	public swim() => ()
	{
	    Console.printLine("This " # this->type # " jumps above the waves!"); 
	}
    }

 

.. code-block:: shadow 
    :linenos: 

    import shadow:io@Console;

    class tutorials:polymorph@Turtle is SeaCreature
    {
        public create(String t, String o)
	{
	    super(t,o); 
	}
	
	public swim() => ()
	{
	    Console.printLine("This " # this->type # " glides through the water!"); 
	}
    }

Lastly, the driver program and console output are provided below. 

.. code-block:: shadow 
    :linenos: 

    SeaCreature creature = SeaCreature:create("Creature", "Arctic"); 
    creature.swim(); 
		
    SeaCreature dolphin = Dolphin:create("Dolphin", "Atlantic"); 
    dolphin.swim(); 
		
    SeaCreature turtle = Turtle:create("Turtle", "Pacific"); 
    turtle.swim(); 

.. code-block:: console

    This Creature is swimming!
    This Dolphin jumps above the waves!
    This Turtle glides through the water!

Before we delve into **polymorphism**, make sure to read through the classes above and the console output. If the information does not look familiar, it would be a good idea to revisit the :ref:`inheritance tutorial<Classes: Inheritance>` before continuing. 

Static vs Dynamic Type
^^^^^^^^^^^^^^^^^^^^^^
In the **driver program**, the **static type** of each object is ``SeaCreature``. An object’s static type (seen on the left side of the equals sign) is the type that is checked at **compile time**. 

When would you get a compile error? Let’s say that ``Dolphin`` has a method called ``dive()`` that ``SeaCreature`` does not, and we made the method call ``dolphin.dive()``. **This code would not compile** because the static type of ``dolphin`` is ``SeaCreature``, and ``SeaCreature`` does not have a ``dive()`` method. Even though **dynamic type** of ``dolphin`` is   ``Dolphin`` (has the ``dive()`` method), it does not matter because **static type** is what is checked at compile time. An object’s **dynamic type**, seen on the right side of the equals sign, is what is checked at **run time**. 

.. note:: The error message would be: ``Undefined symbol: Method dive not defined in this context``

This concept of **dynamic type** leads us into the next point. Look at **Lines 4-8** in the driver program. We call ``swim()`` on both ``dolphin`` and ``turtle``. You may be asking yourself, how do we know which ``swim()`` method will be executed -- the one in ``SeaCreature`` or the overridden one in ``Dolphin``/``Turtle``? Although the static type determines if the program will compile, the object’s dynamic type determines which method will run. For ``dolphin``, its dynamic type is ``Dolphin``, so the ``swim()`` method in that class will run. The same goes for ``turtle``; its dynamic type is ``Turtle``, so the swim method in ``Turtle`` will run, as seen in the console output. This is a prime example of **polymorphism** in action. Both ``turtle`` and ``dolphin`` share the same type, but perform different actions when ``swim()`` is called on them. 


Casting
^^^^^^^

**Casting** is another feature of Shadow that also demonstrates **polymorphism**. In basic terms, **casting** is when we change the type of any object to another compatible type.  
 
The general syntax for casting is as follows: 

``cast<typeCastingTo>(referenceBeingCast)``

Using the ``SeaCreature``, ``Dolphin``, and ``Turtle`` classes above, consider the following example: 

.. code-block:: shadow

    SeaCreature creature2 = cast<SeaCreature>(turtle); 
    creature2.swim(); 
		

Here, the first statement on the right side of the equals sign is the *cast*. We are casting a pre-existing ``turtle`` object into the type ``SeaCreature`` (This would have worked the same way if the static type of ``turtle`` had been either ``SeaCreature`` or ``Turtle``) Why does this work? Recall the idea of an **is-a** relationship from the :ref:`inheritance tutorial<Classes: Inheritance>`. Since ``Turtle`` **extends** ``SeaCreature``, a ``Turtle`` object is *always* a ``SeaCreature`` and therefore can be cast to the type of its parent class without error. This is called **widening** (going from a more narrow class to a broader one). 

Now look at the second statement. Which ``swim()`` method do you think will run? The one from ``SeaCreature``, or the one from ``Turtle``? Since we have cast ``turtle`` into a ``SeaCreature``, your instinct might be to say that the ``SeaCreature`` version of swim will run. However, the ``swim()`` method from ``Turtle`` is actually executed. Even though ``turtle`` has been cast to a ``SeaCreature``, it still does not change the fact that its dynamic type is ``Turtle``. 

Suppose we wanted to cast a ``SeaCreature`` into a ``Turtle`` as shown below. Would this compile?


.. code-block:: shadow

    Turtle turtle2 = Turtle:create("Snapping Turtle", "Atlantic"); 
    turtle2 = cast<Turtle>(creature); 

Although the code would compile (syntax of the cast is correct), it would cause a runtime error, ``CastException``, because the type ``SeaCreature`` is not compatible with ``Turtle`` when you are trying to cast ``SeaCreature`` to ``Turtle``. This is called **narrowing**. Why? Once again think about an **is-a** relationship. While a ``Turtle`` object is always a ``SeaCreature``, a ``SeaCreature`` *could* be a ``Turtle``, but it could also be a ``Dolphin``. You are trying to go from a broad type to a more specific one.  Thus, the statement is ambiguous and we get a runtime error. 

It is also worth mentioning that **side-casting** in Shadow is **always illegal**. For example, you cannot cast a ``Turtle`` to a ``Dolphin`` or vice versa, despite the fact that they are both subclasses of ``SeaCreature``.

Lastly, as a final note on casting, since ``Object`` is the root class for all ``Classes``, you can always cast an object to type ``Object``. See the example below. 


.. code-block:: shadow

    String s = "Help me";		
    Object o = cast<Object>(s);







