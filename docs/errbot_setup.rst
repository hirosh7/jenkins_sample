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
   source /home/hirosh7/PycharmProjects/chatops/venv/bin/activate

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
'secops_sandbox Slack channel <https://hausblackandwhite.slack.com/messages/C9MHM5TEF/>`_. Befor that though we should
do the recommended customization to the **'config.py'** file.



