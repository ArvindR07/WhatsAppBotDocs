Welcome to WhatsAppBot's documentation!
========================================

**WhatsAppBot** is a Python package to automate the process of sending and replying to WhatsApp messages. It uses PyAutoGUI to acheive clicking of mouse events, type messages, select and copy messages, etc.

.. default-role:: code

Creating an instance using constructor
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
newMessagesThere(self)
=============================

Function Description and Working:

This Functions returns a boolean value (True or False).
If there are new messages (unread messages), it returns True, otherwise False.
It uses the red color notification dot on WhatsApp icon to acheive this.
So this function is available only for WhatsApp Desktop Application in Windows and Mac, and not for WhatsApp Web.

Usage:

.. code:: python

   WTBot.newMessagesThere()

Returns:

.. code:: python
   
   # if there are unread messages yet to be opened
   >> True
   
   # if all messages are read and there is no new message
   >> False


=============================
getNewMessages(self)
=============================

Function description and working:

It opens WhatsApp and turns on the unread chat filter. It then opens chats under the filter one by one untill there is nothing left. For each chat, it first scrolls down till the end of chat, while intelligently noting how much it has scrolled down. It then opens contact info (or group info) to copy information about the sender. It closes the contact info and selects messages. It copies it to the clipboard and parses it discard previously read messages and returns the new messages in the below format. After reading all messages it minimizes WhatsApp.

Usage:

.. code:: python

   WTBot.getNewMessages()

Return Template:

.. code:: python
   
   [
      ["Group Chat", group_name, [date_time_string, user_name, phone_number, msg]],
      ["Personal Chat", user_name, phone_number, [date_time_string, msg]],
      ...,
      ...
   ]

It returns a list of new messages clubbed together with the chat.
Must make it clear it is list of messages, give example. 
Above it template.
Order may be different, check...

Return Example:

.. code:: python
   
   [
      ["Group Chat", 'Sample Group 1', 
         [
            ['2023-01-01 15:30', 'nanda', '+91 99524 02150', 'Hi I am Nanda'],
            ['2023-01-01 15:31', 'niresh', '+91 99524 02623', 'Hi I am Niresh'],
            ['2023-01-01 15:34', 'nanda', '+91 99524 02150', 'Good Morning']
         ]
      ],
      ["Personal Chat", 'nanda', '+91 99524 02150', 
         [
            ['2023-01-01 15:30', 'Where are you?'],
            ['2023-01-01 15:31', 'Have you reached home?'],
            ['2023-01-01 15:31', 'Call me back']
         ]
      ],
      ...,
      ...
   ]

=============================
sendMessage(self, personal_or_grp, message_to, message_type, text, image_location)
=============================

This function opens WhatsApp, searches **message_to** and opens it. It it then sends text or image as specified.

Usage:

.. code:: python

   WTBot.sendMessage(personal_or_grp, message_to, message_type, text, image_location)

Arguments:

.. code:: python
   
   # It specifies whether message_to is a group chat or personal chat
   personal_or_grp = 'Personal Chat' or 'Group Chat' 
   
   # message_to is a string
   if personal_or_grp is 'Personal Chat':
      # message_to can be contact name of the personal chat
      # or phone number of the personal chat as string
      
      # contact name and phone number must be exactly same as it is in contact info of whatsapp
      # '9952402150' -> wrong
      # '+91 99524 02150' -> correct
      # '6374681767' -> wrong
      # '+91 6374 681 767' -> correct
   else if personal_or_grp is 'Group Chat':
      # message_to is the name of group
   
   # message_type indicates whether type of message to send is either Image or Text
   message_type = 'Text' or 'Image'
   
   if message_type = 'Text':
      # text argument contains the text to send as string
   else if message_type = 'Image':
      # Image argument contains the path to image loaction as string
      
      # Windows supports all types of image format
      # In Mac, you can only send images in jpeg format
      # In other platforms, sending image is not possible, while you can still send text messages
   
Example:

.. code:: python
   
   WTBot.sendMessage(personal_or_grp='Personal Chat', message_to='+91 99524 02150', message_type='Text', text='hello how are you')
   WTBot.sendMessage(personal_or_grp='Personal Chat', message_to='Nanda', message_type='Text', text='hello how are you')
   WTBot.sendMessage(personal_or_grp='Group Chat', message_to='Group Name', message_type='Image', image=r'C:\Users\nanda\Downloads\dhoni.jpeg')
   

=============================
sendMultipleMessages(self, list_of_replies):
=============================

This function does the same as functionality as sendMessage, but is highly optimised when sending multiple messages. You can buffer the send operations, and give it to this function as a list.

Usage:

.. code:: python

   WTBot.sendMultipleMessages(list_of_replies)

Arguments:

.. code:: python
   
   # list_of_replies is in the below format
   list_of_replies = [
                        ['Personal Chat',ph_no_or_name,[
                                                         [msg1_type,msg1],
                                                         [msg2_type,msg2],
                                                         [msg3_type,msg3],
                                                         .....
                                                        ]
                        ],
                        ['Group Chat',group_name,[
                                                   ['Image',img_location],
                                                   ['Text',text_msg]
                                                  ]
                        ],
                        [....],
                        [....],
                        ...
                     ]
   
Example:

.. code:: python
   
   # list_of_replies is in the below format
   list_of_replies = [
                        ['Personal Chat','+91 99524 02150',[
                                                            ['Text','Hi'],
                                                            ['Text','Hello']
                                                           ]
                        ],
                        ['Group Chat','Sample Group 1',[
                                                         ['Image','C:\\Users\\nanda\\Downloads\\dhoni.jpeg'],
                                                         ['Text','How is it?']
                                                       ]
                        ]
                     ]



