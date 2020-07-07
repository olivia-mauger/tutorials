Interfaces Intro
----------------
In this section we will cover another very important part of **Shadow**: interfaces. In a broad sense, an **interface** is like a contract with a class: it is made up of one or more methods that the class is required to provide implementation for. For example, consider the following simple interface: 

.. code-block:: shadow 
    :linenos: 

    interface CanVacation
    {
        takeVacation() => (); 
    }

Basic Syntax
^^^^^^^^^^^^

The syntax for creating interfaces is very simple. Instead of using the reserved word ``class``, we use ``interface InterfaceName`` in the header, as seen in **Line 1**. Then, in the body of the interface, there should be a collection of one or more method headers, **without any implementation provided**. 

As illustrated in **Line 3**, there are a few differences between method headers in an interface and those in regular classes. For one, interface methods cannot be marked ``public``, ``private``, or ``protected`` because they will **always be public by definition.** The whole purpose of an interface is to require a class to implement its methods, which would not be possible if a method was marked as ``private``. However, interface methods **can** be marked as ``readonly``. Lastly, the method header must end with a semicolon and should not include braces. 

Naming
^^^^^^

By convention, interface names usually begin with ``Can`` and then some word(s) which suggests the ability that the interface ensures. For example, based on the interface name ``CanVacation`` and its single method, ``takeVacation()``, it is reasonable to assume that the classes that implement this interface have the ability to "take a vacation."


