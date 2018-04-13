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










