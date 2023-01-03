Welcome to WhatsAppBot's documentation!
========================================

**WhatsAppBot** is a Python package to automate the process of sending and replying to WhatsApp messages.

.. default-role:: code

Creating an instance
=======================

To create a new setup, run the below script.

.. code:: python
   
   from WhatsAppBot import *
   
   WTBot = WhatsAppBot('create a new setup')

An installer will appear which will guide you through the setup process. 
It is **highly recommended** to watch `this <https://www.youtube.com/>`_ video on how to setup. 

.. image:: setup.png
   :width: 600

After setting up, use the setup name you entered during the setup process to create an instance.

.. code:: python
   
   from WhatsAppBot import *
   
   WTBot = WhatsAppBot('setup name you entered')

Functions
=======================

=============================
newMessagesThere()
=============================

This Functions returns a boolean value (True or False). If there are new messages (unread messages), it returns True. It uses the red color notification dot on WhatsApp icon to acheive this. So this function is available only for WhatsApp Desktop Application in Windows and Mac, and not for WhatsApp Web.

Usage:

.. code:: python

   WTBot.newMessagesThere()

Returns:

.. code:: python
   
   >> True
   >> False


=============================
Function_1
=============================

The given function does this....

Sample call:

.. code:: python

   WBinstance.Function_1(arg1, arg2)

Arguments

.. code:: python
   
   arg1 - 
   arg2 - 

Return Value

.. code:: python
   
   [[val1, val2, val3]]
   
   val1 - 
   val2 - 
   val3 -
