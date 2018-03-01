Mail Server Setup
=================
To confirm proper email generation from all the various pipeline tools, it make sense
to set up a local mail server so we can have local email addresses to use. For this we'll set up a LAN based email
service based on **Postfix**. The details are provided at `GitHubGist <https://gist.github.com/raelgc/6031274>`_.
The instructions specify setting up a **localhost.com** email domain but since this is a Wakanda server, we'll set up a
**wakanda.com** email domain instead.

.. code:: bash

   # Point localhost.com to your machine
   # edit /etc/hosts file to make the domain wakanda.com point to your machine,
   # including this content to the file:

   127.0.0.1 wakanda.com

   # Install Postfix
   sudo apt-get install postfix

   # Two prompts will appear. For the first, select **local only**. For the second, select the **System mail name**.
   # Here I selected **wakanda.com**

   # Configure a catch-all address
   # Create file /etc/postfix/virtual
   sudo nano /etc/postfix/virtual

   # Add the following 2 lines content, replacing with your user account where <your-user> = **hirosh7**
   @wakanda hirosh7
   @wakanda.com hirosh7

   # Configure postifx to read the /etc/postfix/virtual file
   sudo nano /etc/postfix/main.cf

   # Check if the following line is enabled. If not add it
   virtual_alias_maps = hash:/etc/postfix/virtual

   # Activate it via
   sudo postmap /etc/postfix/virtual

   # Reload postfix via
   sudo systemctl restart postfix

Install and Configure Thunderbird
---------------------------------

.. code:: bash

   # Install Thunderbird (typically on Ubuntu this is already installed)
   sudo apt-get install thunderbird

* Skip the welcome screen (click in the button to use existing accounts);
* Click in the Settings button at top right (similar to Chrome settings) then click on Preferences > Account Settings
* Under Account Actions choose **Add Other Account**
* Select **Unix Mailspool (Movemail)**

  - Your account will be hirosh7@wakanda.com

* Ingoing and Outgoing server will be: localhost
* Restart (close and reopen) Thunderbird

Start The Mail Spool File
-------------------------
This step has two purposes:

1. Test your install
2. Stop the **Unable to locate mail spool file** message

Using Thunderbird:

* Send new email to hirosh7@wakanda.com
* Click on **Get Mail**
* Test catch-all

  - send new email to okoye@wakanda.com

* Click on "Get Mail" and you'll see the message at Inbox.

You should now be set up for all pipeline tools to send emails to your development account
(i.e. hirosh7@wakanda.com)




