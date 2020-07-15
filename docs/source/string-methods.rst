String Methods
--------------

This brief tutorial will cover some commonly used methods of the ``String`` class. Each explanation is followed by a coded example. However, this is not an all-inclusive list. To see a complete list of all ``String`` methods, visit the Shadow API. 

toInt()
^^^^^^^

The ``toInt()`` method takes a ``String`` as a parameter and returns an ``int`` representation of a ``String``. There is also a ``toDouble()`` method, which works in the same way, except it returns a ``double``. 


.. code-block:: shadow 

    var word = "6"; 
    var number = word.toInt();
    //Now number holds the int 6

toLowerCase()
^^^^^^^^^^^^^

``toLowerCase()`` takes a ``String`` as a parameter and returns another ``String``, with all letters in uppercase. There is also a ``toLowerCase()`` method that converts all letters to uppercase. 

.. code-block:: shadow 
    
    var yell = "YELLING"; 
    Console.printLine(yell.toLowerCase());  
    // "yelling" is displayed on the console

subtring()
^^^^^^^^^^

``substring()`` is an overloaded method. One version takes in two ``int`` values that represent the starting and ending indices of a ``String``. For example, in the word "hi", "h" has index 0 and "i" has index one. The method then returns a ``String`` with all characters from (and including) the starting index to the ending index (excluding the character at this index). 

The other version takes in one ``int`` representing a starting index. All characters starting from (and including) this idex until the end of the ``String`` are returned. 


.. code-block:: shadow 

    var music = "Rock n Roll"; 
    var second = music.substring(0,5); 
    var first= music.substring(7); 
    Console.printLine(first.concatenate(second)); 
    // "RollRock" is displayed on the console

