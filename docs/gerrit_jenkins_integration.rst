Gerrit / Jenkins Integration
============================

With Jenkins and Gerrit setup and configured, we now want to integrate the two so that when a change is pushed to
Gerrit, it is picked up by Jenkins, built, tested and the results are reported back to Gerrit as a +2, -1, etc.

We'll try the tutorial `Continuous Integration Setup Using Gerrit and Jenkins
<https://www.promptcloud.com/blog/continuous-integration-setup-gerrit-jenkins>`_ for our initial setup.

This tutorial covers many install steps that we've previously executed, so we'll start with the section where we need
to create a jenkins user in Gerrit. Since we'll also need to generate SSH credentials for this user, we'll need to
create a jenkins user on the server first

.. code:: bash

    # create new Gerrit jenkins user
    sudo adduser jenkins
    sudo su jenkins
    cd /home/jenkins

    ssh-keygen -t rsa

Now add a **'jenkins'** user to Gerrit similar to how you've added other Gerrit users and copy in the just generate
ssh key and verify connectivity

.. code:: bash

   cat .ssh/id_rsa.pub

   # Copy this key into the Gerrit jenkins user set-up

   # Verify connectivity
   ssh jenkins@wakanda -p 29418

You should see connect success message which confirms our set up is ready to go.

Now over in Jenkins, we want to create a new pipeline job.
