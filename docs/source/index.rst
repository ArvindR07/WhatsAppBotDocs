Welcome to WhatsAppBot's documentation!
========================================

**WhatsAppBot** is a Robotic process automation package to automate the process of reading and replying to WhatsApp messages. It uses PyAutoGUI for performing keyboard and mouse events, using which messages are selected, copied and typed.
Watch `this <https://www.youtube.com/>`_ 2 minute animated video on WhatsAppBot. 

.. default-role:: code

Installation and Dependency
=======================

**Installation in Windows:**

.. code:: python
   
   pip install WhatsAppBot-Nanda[win32]


**Installation in other Platforms:**

.. code:: python
   
   pip install WhatsAppBot-Nanda
   
**Dependency for Mac:**
Our package is dependent on PyAutoGUI, and in some Mac systems, few of its functions does not work.
To check whether you can install WhatsAppBot in your Mac, do the following steps.

1. Install PyAutoGUI on your Mac using the below command

.. code:: python
   
   python3 -m pip install pyautogui

2. Then run the following function code snippet

.. code:: python

   import pyautogui
   pyautogui.displayMousePosition()

If you get an output similar to the one below, WhatsAppBot will work in your system.

.. code:: python

   Press Ctrl-C to quit.
   X:  0 Y: 1027 RGB: ( 108,  7,  3)
   
But if you get an output similar to the one below, WhatsAppBot will not work in your system.

.. code:: python

   Press Ctrl-C to quit.
   X:  0 Y: 1027 RGB: ( NaN,  NaN,  NaN)
   
  
Creating an instance using constructor
=======================

| WhatsAppBot is a Robotic process automation package that imitates human behaviour with WhatsApp Application in PC/Desktop, and it needs few coordinates of your system, to perform the operations. 
| For example, to send a new message, the package needs to know where the type message box coordinated are located as well as the send button.
| To create a new setup, run the script given below. It will open a setup box (Installer) with neat User Interface that will guide you with the necessary steps. 

.. code:: python
   
   from WhatsAppBot import *
   
   WTBot = WhatsAppBot('create a new setup')

 
It is **highly recommended** to watch `this <https://www.youtube.com/>`_ video on how to setup.
You just have to setup once and the entire setup process takes only about 5 to 10 minutes

.. image:: setup.png
   :width: 600

| One thing you will be asked to do in the setup process is to create an empty group with some name.
| This will serve as a default group. The use of this group is explained later in this documentation.
| After setting up, use the setup name you entered during the setup process to create an instance.

.. code:: python
   
   from WhatsAppBot import *
   
   WTBot = WhatsAppBot('setup name you entered')

| When creating an instance of WhatsAppBot by running the above code snippet, WhatsApp in your system is opened.
| It then goes into the chat of default group and minimises WhatsApp. Again the purpose of this is explained later.

Functions
=======================

Watch `this <https://www.youtube.com/>`_  15 minute video that gives a demo on how to use all the functions of WhatsAppBot given below.

=============================
newMessagesThere(self)
=============================

**Function Description and Working:**

| This Functions returns a boolean value (True or False).
| If there are new messages (unread messages), it returns True, otherwise False.
| It uses the red color notification dot on WhatsApp icon to acheive this.
| This function is available only for WhatsApp Desktop Application in Windows and Mac, and not for WhatsApp Web.
| 

**Usage:**

.. code:: python

   WTBot.newMessagesThere()

**Returns:**

.. code:: python
   
   # if there are unread messages yet to be opened
   >> True
   
   # if all messages are read and there is no new message
   >> False


=============================
getNewMessages(self)
=============================

**Function description and working:**

| It opens WhatsApp and turns on the unread chat filter.
| It then opens chats under the filter one by one untill there is nothing left.
| For each chat, it first scrolls down till the end of chat, while intelligently noting how much it has scrolled down.
| It then opens contact info (or group info) to copy information about the sender.
| After that it closes the contact info and drags and selects messages.
| It copies it to the clipboard and parses it to discard previously read messages and returns the new messages in the format given below in this documentation.
| The logic for discarding old messages that are copied is taken care and you only get new messages.
| In the internal implementation, this is done by storing the old messages in your system.
| After reading all messages it goes into the default group and minimizes WhatsApp.
|

**Reason for having Default Group:**

| The reason for going inside default group is, to go into the chat that has new messages, we need it to be unread.
| So when unread chat filter is turned on, we can go into the chat and copy new messages.
| If this is not done, we may miss new messages.
|

**Scenario Explained using Example:**

| Assume we get a new message from CHAT A. 
| When getNewMessages() function is called, WhatsApp is opened and after turning on unread chat filter we go into CHAT A and new messages are copied.
| Assume we don't go into default group and we minimise WhatsApp.

| Now after some time, new message has come from CHAT A.
| If we call getNewMessages(), when WhatsApp is opened, we will be inside CHAT A, and we would have read new messages from CHAT A.
| So when unread chat filter is turned on, we won't have CHAT A, as it would have been read.
| This means we lose the message.
| That's why we go inside the default group in the end.
| This is the same reason why when creating an instance of WhatsAppBot, we go inside default group
|


**Usage:**

.. code:: python

   WTBot.getNewMessages()

**Return Template:**

.. code:: python
   
   [
      ["Group Chat", group_name, [date_time_string, phone_number, user_name, msg]],
      ["Personal Chat", user_name, phone_number, [date_time_string, msg]],
      ...,
      ...
   ]

It returns a list of new messages clubbed together with the chat.


**Return Example:**

.. code:: python
   
   [
      ["Group Chat", 'Sample Group 1', 
         [
            ['2023-01-01 15:30', '+91 99524 02150', 'nanda', 'Hi I am Nanda'],
            ['2023-01-01 15:31', '+91 99524 02623', 'niresh', 'Hi I am Niresh'],
            ['2023-01-01 15:34', '+91 99524 02150', 'nanda', 'How are you Niresh?']
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

This function opens WhatsApp, searches the name of contact or group to whom the message is to be sent and opens it. It then sends text or image as specified. If there is no such contact or group, it does not send anything. Then in the end it goes into the default group and minimises WhatsApp.

**Usage:**

.. code:: python

   WTBot.sendMessage(personal_or_grp, message_to, message_type, text, image_location)

**Arguments:**

1. personal_or_grp:
      Objective: Specify the type of chat
      
      Values: "Personal Chat", "Group Chat"
2. message_to:
      Objective: To whom the message is being sent to. If it "Personal Chat", then it can be a string representing the full name of the contact as saved, or phone number in the same format as in WhatsApp, and if it is "Group Chat" the full name of the group (case sensitive)
      
      Values: Phone Number (or) Contact Name/ Group Name (Type: String)
              
              '6374680762'       -> wrong
              
              '+91 6374 680 762' -> correct
3. message_type:
      Objective: Specify the type of message
      
      Values: "Text", "Image"
4. text:
      Objective: The text that needs to be sent, (message_type should be set as "Text")
      
      Values: The message in String format
5. image_location:
      Objective: The path to the image that needs to be sent, (message_type should be set as "Image")
      
      Values: The path to the image in String format
               
      Note: (Windows supports all image formats, Mac only supports .jpeg)
   
**Example:**

.. code:: python
   
   WTBot.sendMessage(personal_or_grp='Personal Chat', message_to='+91 99524 02150', message_type='Text', text='hello how are you')
   WTBot.sendMessage(personal_or_grp='Personal Chat', message_to='Nanda', message_type='Text', text='hello how are you')
   WTBot.sendMessage(personal_or_grp='Group Chat', message_to='Group Name', message_type='Image', image_location=r'C:\Users\nanda\Downloads\dhoni.jpeg')
   

=============================
sendMultipleMessages(self, list_of_replies):
=============================

| This function does the same functionality as sendMessage, but is highly optimised when sending multiple messages.
| You can buffer the send operations, and give it to this function as a list in the below given format. Use this if you want to send multiple messages.
| It is faster as it does not go into the default group after each send operation
| Assume you want to send 10 messages. If you use sendMessage, for each operation, WhatsApp will be opened, the chat to which message is to be sent will be opened, message will be sent, default group will be opened and WhatsApp will be closed.
| But if you use sendMultipleMessages, WhatsApp will be opened, all the send operations will be done and at the end only, default group will be opened and WhatsApp will be minimised.
| So for 10 messages, we can save time for (opening WhatsApp, going to default group, minimizing WhatsApp) x 9 times.


**Usage:**

.. code:: python

   WTBot.sendMultipleMessages(list_of_replies)

**Arguments:**

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
   
**Example:**

.. code:: python
   
   # list_of_replies is in the below format
   list_of_replies = [
                        ['Personal Chat','+91 99524 02150',[
                                                            ['Text','Hi'],
                                                            ['Text','Hello']
                                                           ]
                        ],
                        ['Personal Chat','Nanda',[
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


=============================
getPreviousMessages(count, personal_or_grp, ph_no_or_name, message_type, start_date_time, end_date_time)
=============================

This function returns the previously sent and received messages as list sorted by the date-time of the message (earliest to latest) [start_date_time to end_date_time] . The arguments to the functions are various filters you can use.
Note: You will only get messages that were read or sent by using the package. That means only the messages that were sent using WTBot.sendMessage() and read using WTBot.getNewMessages() will be available

**Usage:**

.. code:: python

   getPreviousMessages(count, personal_or_grp, ph_no_or_name, message_type, start_date_time, end_date_time)

**Arguments:**

1. count:
      Objective: maximum number of records to be returned
      
      Values: Integer value
      
      Default: 100
      
2. personal_or_grp:
      Objective: Filter only Personal Chat messages or Group Chat messages or return Both
      
      Values: "Personal Chat", "Group Chat"
         
      Default: None ->  meaning no filter is applied and both types are returned
3. ph_no_or_name:
      Objective: Filter based on Phone Number or Contact Name if it is "Personal Chat" or with Group name if it is "Group Chat"
      
      Values: Phone Number (or) Contact Name, (Type: String), or Group Name
             
      Default: None -> meaning no filter is applied
4. message_type:
      Objective: Specify the type of message
      
      Values: "Text", "Image"
      
      Default: "Both"
5. start_date_time:
      Objective: Specify start date
      
      Values: Date in 'YYYY-MM-DD HH:MM' format 
      Default: '1970-01-01 00:00'
6. end_date_time:
      Objective: Specify end date
      
      Values: Date in 'YYYY-MM-DD HH:MM' format
      Default: '3000-01-01 00:00'
   
**Example:**

.. code:: python
   
   WTBot.getPreviousMessages(count, personal_or_grp, ph_no_or_name, message_type, start_date_time, end_date_time)
   WTBot.getPreviousMessages(count, personal_or_grp, ph_no_or_name, message_type, start_date_time, end_date_time)
   WTBot.getPreviousMessages(count, personal_or_grp, ph_no_or_name, message_type, start_date_time, end_date_time)

**Return Template:**

.. code:: python
   
   "Group Chat", msg_type = Received, group_name, date_time_string, user_name, phone_number, msg
   "Group Chat", msg_type = Sent, group_name, date_time_string, msg
   "Personal Chat", msg_type = Sent/Received, user_name, phone_number, date_time_string, msg



**Return Example:**

.. code:: python
   
   [
   [],
   [],
   []
   ]

=============================
changeTimeDelays(waiting_time_delay, mouse_delay, typing_delay)
=============================

**Function Description and Working:**

This is used to change the time delays of an already existing setup. All the 3 arguments have a default parameter as None, so you can change just one or two of them as you please. All 3 arguments take only float.

**Usage:**

.. code:: python

   WTBot.changeTimeDelays(waiting_time_delay, mouse_delay, typing_delay)

**Example:**

.. code:: python
   
   WTBot.changeTimeDelays(waiting_time_delay=0.5, mouse_delay=0.5, typing_delay=0.01)
   WTBot.changeTimeDelays(waiting_time_delay=0.75, typing_delay=0.01)
   WTBot.changeTimeDelays(typing_delay=0.1)
   ..........
     
=============================
resetWhatsappBot(self)
=============================

**Function Description and Working:**

This function deletes all the previously read and sent messages. So once you call this, the getPreviousMessages() function returns empty list (untill ofcourse when new messages are read using getNewMessages(), and sent using sendMessage().
Call this function when you want to discard old messages and start afresh.

**Usage:**

.. code:: python

   WTBot.resetWhatsappBot()

   



