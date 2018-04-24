Gerrit Setup
============

I initially tried to run Gerrit in a docker container, but hit two issues:

1) The number of containers I was running was eating up too much RAM

2) I couldn't figure out how to persist Gerrit data across container restarts

So I'm going old school and installing Gerrit on bare metal

The details I'm following are `here <https://gerrit-review.googlesource.com/Documentation/install-quick.html>`_

One update I had to make was to switch the default Gerrit port from 8080 to 8081 just like in the container version.
To do this I edited **~/gerrit_testsite/etc/gerrit.config** and changed the following

.. code:: bash

   [gerrit]
       basePath = git
       serverId = 16c006cd-849e-4e32-a42d-bcfd0caa0800
       canonicalWebUrl = http://Wakanda:8081/

   [httpd]
       listenUrl = http://*:8081/

I also had to simplify authentication. The default OpenID option was a little problematic. There seemed to be no easy way
to set up a separate authenticated admin account. Default setting is to set up the first added user with admin
 privileges which is not what I wanted, so I went with

.. code:: bash

   [auth]
        type = DEVELOPMENT_BECOME_ANY_ACCOUNT

as documented in `the auth guide <https://gerrit-review.googlesource.com/Documentation/config-gerrit.html#auth>`_.

.. warning::
   This authentication setting is ONLY for development. When moving to production, choose one of the standard options
   like **OpenID** or **OAuth**.

Gerrit is installed as a service so you can use the following to start and stop Gerrit

.. code:: bash

   ~/gerrit_testsite/bin/gerrit.sh start
   ~/gerrit_testsite/bin/gerrit.sh stop
   ~/gerrit_testsite/bin/gerrit.sh restart

So to commit the config file change, I restarted the Gerrit service

.. note::
   If any configuration changes are made to Gerrit via the /etc/gerrit.config file, you must restart the Gerrit
   service for those changes to take effect.

Configuring Gerrit
------------------

Creating another Gerrit User
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

   # create new Gerrit user tchalla
   sudo adduser tchalla
   sudo su gerrit
   cd /home/tchalla

   ssh-keygen -t rsa

   # follow along with the rest of the instructions highlighted above (Gerrit Quick Install)

Importing a project into Gerrit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Text here


