Welcome to WhatsApp Bot's documentation!
========================================

**WhatsAppBot** (/lu'make/) is a Python library to automate the functions of the WhatsApp application.

.. default-role:: code

=======================
Functions
=======================

Function_1
=============================

The given function does this....

Sample call:

.. code:: python

   WBinstance.Function_1(arg1, arg2)

Arguments

.. code::
   print(x)

Return Value

.. code::
   [[val1, val2, val3]]
   
   val1 - 
   val2 - 
   val3 -

For example:

.. code:: python

    >>> pyautogui.size()
    (1920, 1080)
    >>> pyautogui.position()
    (187, 567)

Here is a short Python 3 program that will constantly print out the position of the mouse cursor:

.. code:: python

    #! python3
    import pyautogui, sys
    print('Press Ctrl-C to quit.')
    try:
        while True:
            x, y = pyautogui.position()
            positionStr = 'X: ' + str(x).rjust(4) + ' Y: ' + str(y).rjust(4)
            print(positionStr, end='')
            print('\b' * len(positionStr), end='', flush=True)
    except KeyboardInterrupt:
        print('\n')
