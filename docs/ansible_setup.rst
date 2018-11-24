Ansible Setup
=============

We'll use Ansible as our Infrastructure as a Service (IaaS) to auto setup our test staging environment so we'll
experiment with installation and validation tests in this section. Most info here is pulled from the
`official Ansible 2.7 documentation <https://docs.ansible.com/ansible/latest/index.html>`_.

Installation
~~~~~~~~~~~~
Ubuntu installation is straight-forward. Ubuntu builds are available in a PPA here.

To configure the PPA on your machine and install ansible run these commands:

.. code:: bash

   $ sudo apt-get update
   $ sudo apt-get install software-properties-common
   $ sudo apt-add-repository --yes --update ppa:ansible/ansible
   $ sudo apt-get install ansible

   # Verify install
   $ ansible --version

   # output should look similar to the following

   ansible 2.5.1
   config file = /etc/ansible/ansible.cfg
   configured module search path = [u'/home/hirosh7/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
   ansible python module location = /usr/lib/python2.7/dist-packages/ansible
   executable location = /usr/bin/ansible
   python version = 2.7.15rc1 (default, Apr 15 2018, 21:51:34) [GCC 7.3.0]

Setting up servers and server connectivity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Details from this section come from `Ansible: Post-Installl Setup instructions
<https://hvops.com/articles/ansible-post-install/>`_. In summary:

1) Add your target servers to the default /etc/ansible/hosts file
2) Generate your SSH key on your host Ansible server (e.g. ssh-keygen -t rsa -C "name@example.org" -
   **Don't specify a passkey**)
3) Copy your public SSH key to your target servers (e.g. ssh-copy-id user@<target_server>)

To test connectivity:

.. code:: bash

   # Assume your target server(s) are defined in the devserver' group in the /etc/ansible/hosts file
   $ ansible devserver -m ping

   # Sample output
   <target server name> | SUCCESS => {
    "changed": false,
    "ping": "pong"
   }

Testing out a sample playbook
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Before putting together a playbook of plays, you can try out `single (ad hoc) commands
<https://docs.ansible.com/ansible/2.5/user_guide/intro_adhoc.html>`_ to get a feel for the
types of things that can be done. Once you're familiar with a few commands and return data, the next step will be to
code them into a playbook.

Pulling Ansible Playbooks from Github
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
data goes here

