Operators and Expressions
-------------------------

Assignment
^^^^^^^^^^

In the "Variables Introduction" section, assigning a variable a particular value is briefly touched on. For example, consider the following line of code:  

.. code-block:: shadow 

    double height = 5.4; 

In this instance, the variable **height** is *assigned* the value 5.4. Another example would be 

.. code-block:: shadow

    int total = 6 + 6; 

The variable **total** is *assigned* the result of the evaluated **expression** 6 + 6, which is 12. 

While these two examples constitute the basics of assignment, Shadow also has some unique features that help streamline the more complicated examples of assignment. See below. 


.. code-block:: shadow 

    int x; //Line 1
    int y; //Line 2
    int z; //Line 3
    (x, y) = (3, 6); //Line 4
    (x, y) = (y, x); //Line 5
    (x, y, z) = 10; //Line 6

The above section of code demonstrates a few Shadow syntactic structures: **sequences** and two of its subtypes, **swaps** and **splats**. In the first three lines of code, the variables **x**, **y**, and **z**  are declared but not **initialized**. However, in Line 4, variables **x** and **y** are initiated in a single line. This is a basic **sequence**. Line 5 is an example of a **swap** because now **x** has a value  6 and **y** has value 3. Lastly, Line 6 is called a **splat** because all three variables are set to 10 in the same line. 

Arithmetic Operators
^^^^^^^^^^^^^^^^^^^^ 


Arithmetic operators in Shadow appear mostly as they would in an elementary math class. See the list below (in order of precedence).

* "\*" is used for multiplication
* "/" is used for division 
* "%" is used for modular division
* "+" is used for addition
* "-" is used for subtraction


**Precedence with Arithmetic Operators Example** 


