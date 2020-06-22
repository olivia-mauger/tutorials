Reading from the Console
------------------------

Oftentimes when writing code, we want to prompt the user to input some value that we can use in the program. For example, what if you wanted to create a program that calculates someone’s BMI? You would need to first ask the user their height in inches and then their weight in pounds. After storing these values in separate variables, you would be able to perform calculations to output their BMI. 

How is this done? There are 4 main methods used for reading input as seen in the list below: 

* ``readByte``, which returns the next ``byte``
* ``readCode``, which returns the next character as a ``code``
* ``readLine``, which returns the next line of text
* ``readString``, which returns the next white-spaced delimited text 

The following example illustrates some basic implementations of these methods. 

.. code-block:: shadow
    :linenos: 
	

