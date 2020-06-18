Arrays 
------
This page introduces and analyzes **arrays** in Shadow. An array is a very useful data type that is able to store multiple values *of the same type*.  For example, if I had a list of ``String`` variables representing different dog breeds, instead of dealing with all of these individual variables, I could store the literal ``String`` values in a single array. See the visualization of an array below. 

+---------+---------+---------+---------+---------+
|    0    |    1    |    2    |    3    |    4    |
+---------+---------+---------+---------+---------+

Each “box”  represents the location of the data being stored in the array. The numbers demonstrate how arrays are **indexed**. *It is important to remember that the first position is indexed at 0, NOT 1.*  In the dog breed example, each numbered location would correspond to a different dog breed (i.e. At location 0, it could hold “Beagle”). 

Initializing and Displaying an Array
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
There are multiple ways to **declare** and **fill** an array in Shadow.  If you would like to input literal values, or variables of the same type as the array, the declaration is as follows: 

.. code-block:: shadow 
    :linenos:   
		
	var favoriteBreed = "Beagle"; 
	String[] dogBreeds = {favoriteBreed, "Chihuahua", "Poodle", "Pomeranian", "Maltese"}; 
		
	Console.printLine(dogBreeds.toString());
	Console.printLine(dogBreeds); 


Console output: 

.. code-block:: console 

    [Beagle, Chihuahua, Poodle, Pomeranian, Maltese]
    [Beagle, Chihuahua, Poodle, Pomeranian, Maltese]
	
**Basic Initialization** 

**Line 2** highlights the key syntax rules for declaring an array. First, the specified variable type is followed by ``[]`` and the array name. Then, to the right of the equals sign, any literal values or variable names are enclosed by ``{ }`` and separated by commas. Voilà! You have an array. 

.. note:: When you declare an array to be a certain type, all elements in that array *must be of the same type* or you will get a compile error!


**Displaying an Array** 

Finally, **Lines 4 and 5** show two easy ways to nicely format and print out an array. The ``Array`` class has a ``toString()`` method (more on methods for the next topic) that takes an array and outputs its contents in between ``[]``. Although **Line 4** is a valid way to use the method, **Line 5** is a shortcut that produces the same results, as seen in the console output above. 


**Other Methods of Initialization** 

Sometimes, as programmers, we are not able to or do not want to declare and fill an array all at once. Instead, we can specify the array’s **size**: 

For example, 

.. code-block:: shadow 

    int[] golfScores = int:create[5]; 
	
Here, we have created an array called ``golfScores`` that can hold 5 values. *Once an array’s size is set, it cannot change.* Although we haven’t filled the array with golf scores yet, the array is **not empty.** Each index is given the same default value. The default values of frequently used types are listed below: 

* ``int``: ``0``
* ``double``: ``0.0``
* ``String``: ``" "``
* ``boolean``: ``false``
* ``code``: ``' '``

*A Brief Side Note: At this point, you may be wondering why we used the reserved word* ``create`` *when initializing the array. This is because in Shadow, arrays are designed to be “object-like.” Although we will be covering objects later in the tutorials, all you need to know for now is the syntax.* 


Thus, the array ``golfScores`` holds five 0’s. Now you may ask, how do we input the golf scores? Although you cannot change the size of the array once it is created, you can change/update the values of individual elements. The following examples illustrate two possible ways to do so: 

.. code-block:: shadow 
    :linenos:   

    /*
	 * You and your friends, who are extremely novice golfers, decide to go 
	 * play a round of golf one afternoon. Now, you want to
	 * record their scores. 
	 * 
	 * You: 102
	 * Zizi: 104
	 * Omar: 106
	 * Chris: 108
	 * Daphne: 110
	 */
		 
	/*
	 * Here we use a for loop to fill in the scores, 
	 * which happen to each increase by 2. 
	 */
		 
	var index = 0; 
	for(int i = 102; i <= 110; i += 2) 
	{ 
	golfScores[index] = i; 
	index += 1; 
	}
		 
		 
	/* 
	 * Here we will manually enter the scores. 
	 */
		  
	golfScores[0] = 102; 
	golfScores[1] = 104; 
	golfScores[2] = 106; 
	golfScores[3] = 108; 
	golfScores[4] = 110; 
	
Both of these examples achieve the desired result of putting the golf scores into the ``int`` array. The most important thing to take away is how we accessed specific elements of the array. As mentioned before, an array’s first element is indexed at zero. So, if I wanted to put my score as the first element, I would say ``golfScores[0] = 102;`` (or ``golfScores[index]`` when index equals 0 for the ``for`` loop example). **If you ever need to access individual elements of an array, this is the correct syntax.** i.e. ``var worstScore = golfScores[4];`` Now, ``worstScore`` holds the value 110. 

	
	
		  





