Ubuntu Environment
==================
We'll be setting up a Security DevOps (SecOps) sandbox server to experiment with various DevOps
tools and approaches.

I've installed a dual boot version of Ubuntu 17.10 along side Windows 10 on a new desktop server.
Credential details are in a LastPass secure note titled **Dell SecOps Desktop Server**. Additional
details:

* Server Name: Wakanda
* Server IP: 192.168.1.2

Helpful Ubuntu Commands
-----------------------

Configuring xTerm
~~~~~~~~~~~~~~~~~

 Create a file in your home directory named .Xresources to store your preferences for various X programs.
   Append a line to the file such as

.. code:: bash

   xterm*font:     *-fixed-*-*-*-18-*

This informs xterm to use the 'fixed' font at size 18. From here, you can either restart X or run

.. code:: bash

   xrdb -merge ~/.Xresources

in a terminal to incorporate the changes you've made. All new xterms should now have the font change. If you run
**'man xterm'** and go down to the RESOURCES section, you can find a wealth of additional, configurable xterm options.

Add/Remove Users
~~~~~~~~~~~~~~~~

.. code:: bash

   # add a user
   sudo adduser <user_name>

   # remove a user
   sudo userdel <user_name>

Install a Java JDK
~~~~~~~~~~~~~~~~~~
In order to get Maven to properly compile files, you need to have a JDK installed vs. a JRE. Details for
this section come from this article, `'How to Install Java on Ubuntu'
<https://thishosting.rocks/install-java-ubuntu/>`_

.. code:: bash

   # First update the system
   sudo apt-get update && sudo apt-get upgrade

   # Install the package
   sudo apt-get install default-jdk

   # Check which versions of Java you have installed
   update-alternatives --config java

   Sample Output:
     Selection    Path                                            Priority   Status

    * 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1101      auto mode
      1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1101      manual mode
      2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode

   # To set JAVA_HOME to a new path copy/paste path to exclude 'bin/...'
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64

   # If you're trying to set up Maven to use this, confirm it has picked up this change
   mvn -version

   Sample Output:

   Maven home: /usr/share/maven
   Java version: 10.0.1, vendor: Oracle Corporation
   Java home: /usr/lib/jvm/java-11-openjdk-amd64
   Default locale: en_US, platform encoding: UTF-8
   OS name: "linux", version: "4.15.0-30-generic", arch: "amd64", family: "unix"

  # To make JAVA_HOME update permanent
  nano /etc/environment

  # update $JAVA_HOME variable with new path

Shodan CLI Setup
~~~~~~~~~~~~~~~~

.. code:: bash

   # Installs as part of the python install
   sudo pip install shodan

   # on my Ubuntu system, the executable ended up in ./.local/bin so
   # edit .bashrc and add that to the path
   export PATH=$PATH:./.local/bin

   # Initialize Shodan with your API key. You can find this under
   # your `shodan <(https://www.shodan.io/)>`_ login. Click on 'My Account' once logged in
   shodan init <api-key>

Installing Searchsploit
~~~~~~~~~~~~~~~~~~~~~~~

The following was pulled from the `Exploit-DB web page <https://www.exploit-db.com/searchsploit/#installlinux>`_
for Linux.

“searchsploit”, [is] a command line search tool for Exploit-DB that also allows you to take a copy of Exploit Database
with you, everywhere you go. SearchSploit gives you the power to perform detailed off-line searches through your
locally checked-out copy of the repository. This capability is particularly useful for security assessments on
segregated or air-gapped networks without Internet access.

.. code:: bash

   git clone https://github.com/offensive-security/exploitdb.git /opt/exploitdb

   # Add /opt/exploitdb to ~/.bashrc path
   export PATH=$PATH:/opt/exploitdb

Make Ubuntu do nothing when laptop lid closes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To make Ubuntu do nothing when laptop lid is closed:

1) Open the /etc/systemd/logind.conf file in a text editor as root, for example,

.. code:: bash

   sudo nano /etc/systemd/logind.conf
   # or
   sudo -H gedit /etc/systemd/logind.conf

2) Add a line **HandleLidSwitch=ignore** (make sure it's not commented out!)

3) Restart the systemd daemon with this command:

.. code:: bash

   sudo restart systemd-logind
   # or, from 15.04 onwards:
   sudo service systemd-logind restart

.. tip::
   The first time I did this the laptop display blanked out and didn't turn back on even after closing
   and reopening the lid. A reboot brought it back, but I ended up having to do this by SSH'ing into it from
   another laptop.