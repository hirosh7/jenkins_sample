Ubuntu Sandbox Setup
====================
We'll be setting up a Security DevOps (SecOps) sandbox server to experiment with various DevOps
tools and approaches.

Ubuntu Environment
------------------
I've installed a dual boot version of Ubuntu 17.10 along side Windows 10 on a new desktop server.
Credential details are in a LastPass secure note titled **Dell SecOps Desktop Server**. Additional
details:

* Server Name: Wakanda
* Server IP: 192.168.1.2

Docker Installation
-------------------
First step is to install Docker. I pulled the following details from this `GitHub Gist page
<https://gist.github.com/levsthings/0a49bfe20b25eeadd61ff0e204f50088>`_.

.. code-block:: bash

    sudo apt-get update
    sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo apt-key fingerprint 0EBFCD88

    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu zesty stable"

    sudo apt-get update
    sudo apt-get install docker-ce

The install worked but when trying a test with the command

.. code-block:: bash

    docker run hello-world

It failed and would only run with the **sudo** command. This blows so I took a look at how to fix
this using Docker's `**Post Installation Steps for Linux** page
<https://docs.docker.com/install/linux/linux-postinstall/>`_. Here are the details:

.. code-block:: bash

   # To create the docker group and add your user:

   # Create the docker group.
   $ sudo groupadd docker

   # Add your user to the docker group.
   $ sudo usermod -aG docker $USER

   # Log out and log back in so that your group membership is re-evaluated.
   <ctrl><alt><delete>

   # Verify that you can run docker commands without sudo.
   $ docker run hello-world

Worked like a charm! Docker installed.









