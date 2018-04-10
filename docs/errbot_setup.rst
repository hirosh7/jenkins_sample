Errbot Setup
============
To experiment with ChatOps capabilities, we'll install the Python based Errbot Chatbot.

.. image:: images/errbot_icon.png
   :align: center

Details are pulled from `here <http://errbot.io/en/latest/user_guide/setup.html>`_. Good news is that Python 3 is
already installed on the server (v 3.6.3) so we can just proceed with the Errbot specific install requirements.

Rather than following the instructions to install and setup Errbot via the command line, I set up a new Python 3.6
**'Chatbot'** Pycharm project as follows:

* Create new 3.6 virtual env project ('Chatbot')
* Add errbot package to environment

.. image:: images/chatbot_pycharm_interpreter.png
   :align: center

As you can see, installing errbot pulls in a **bunch** of other packages (which is why it's good to do this in a
virtualenv!)

You can now open a terminal window and source to the chatops virtualenv directory and run a test command.

.. code:: bash

   # Switch to chatops virtualenv
   cd /home/hirosh7/PycharmProjects/chatbot
   source /home/hirosh7/PycharmProjects/chatbot/venv/bin/activate

   # start errbot in interactive mode
   errbot

   # run !tryme command
   >>> !tryme

.. image:: images/errbot_startup_test.png
   :align: center

.. Note::
   You need to hit the 'enter' key **twice** after entering the '!*' command at the errbot prompt in interactive mode
   go get the requested action to occur.

To exit out of the virtualenv when you're done testing

.. code:: bash

   # Exit from Errbot
   <ctrl-c>

   # Exit chatops virtualenv
   deactivate

Customizing and Extending Errbot
--------------------------------
Two things we'll want to do - 1) create plugins for our desired actions and 2) connect to our
`secops_sandbox Slack channel <https://hausblackandwhite.slack.com/messages/C9MHM5TEF/>`_. Before that though we
should do the recommended customization to the **'config.py'** file.

There's a **'config-template.py'** file that has all the details of what can be configured. You'll note the the initial
**config.py** file set up by the **'errbot --init'** command is pretty bare-bones so we'll pull in additional updates
from the 'config-template.py' file. You can find this file in the Pycharm Project window under
**venv->lib->site-packages->errbot->config-template.py**

Based on the instructions, these are the attributes you **absolutely** need to change in your 'config.py' file. Others
you can do later on:

* Check or change **BOT_DATA_DIR**. This is the directory where the bot will store configuration
  data. Confirm that this is set to: /home/hirosh7/PycharmProjects/chatbot/data (or similar in your environment)
* Check or change **BOT_LOG_FILE** to be sure it point to a writeable directory on your system
* Once our errbot is working well, we'll probably also want to change **BOT_LOG_LEVEL** to something other than
  **debug** to keep the log file from flooding.
* The final configuration we must do is setting up a correct **BACKEND** which is set to **Text** by
  'errbot --init' but you can change to the name of the chat system you want to connect to. We'll set this
  to 'Slack' and subsequently   follow the set up details for the `Slack Backend Configuration
  <http://errbot.io/en/latest/user_guide/configuration/slack.html>`_ when done here

  * As part of this we'll need to set the **BOT_IDENTITY** entry to set the credentials Errbot will use to connect to the
    chat system
  * We'll also need to change **BOT_ADMINS** as part of this process given the comment says,
    '# !! Don't leave that to "@CHANGE_ME" if you connect your errbot to a chat system !!' :-)

Slack Backend Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~
We start with installing the python 'slackclient' in our project. Add to the project interpreter setting via the
Pycharm settings option. Alternatively, at the project command line

.. code:: bash

   pip install slackclient

Next we need to `add the bot integration to Slack <https://hausblackandwhite.slack.com/apps/new/A0F7YS25R-bots>`_.
This link will take you to a page similar to the following:

.. image:: images/slack_bot_integration.png

Click the **'Add Bot Integration'** button and that will take you to the bot settings page where you can capture your
bot token and add bot customizations like adding an image and description.

Update the bot project **config.py** file to include a valid admin and the token similar to the following:

.. code:: bash

   BOT_IDENTITY = {
    'token': 'xoxb-4426949411-aEM7...',
   }

   BOT_ADMINS = ('@hirosh7')

To enable using the bot's name in BOT_ALT_PREFIXES for @mentions in Slack, simply add the bot's name as follows:

.. code:: bash

   BOT_ALT_PREFIXES = ('@astrobot',)

.. info::

   If you're using a bot account you should set CHATROOM_PRESENCE = (). Bot accounts on Slack are not allowed to
   join/leave channels on their own (they must be invited by a user instead) so having any rooms setup in
   CHATROOM_PRESENCE will result in an error.

   If you are using a regular user account for the bot then you can set CHATROOM_PRESENCE to a list of channels and
   groups to join.







