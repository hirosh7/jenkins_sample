Tomcat Setup
============
We'll also install Tomcat in a docker container. Some configuration files will need to be changed so we'll start with
the `base Tomcat image <https://hub.docker.com/_/tomcat/>`_ from Docker Hub. Initially we'll just start it up in
interactive mode.

.. code:: bash

   docker run -it --rm -p 8888:8080 --name Tomcat tomcat:8.0

Editing and Saving Image Changes
--------------------------------
Initially, if you try to run the **Manager App** from the Tomcat homepage (which you access at
http://localhost:8888), you'll hit a 401 error with a message like the following:

.. code:: bash

   You are not authorized to view this page. If you have not changed any configuration files, please examine the
   file conf/tomcat-users.xml in your installation. That file must contain the credentials to let you use this
   webapp.

   For example, to add the manager-gui role to a user named tomcat with a password of s3cret, add the following
   to the config file listed above.

   <role rolename="manager-gui"/>
   <user username="tomcat" password="s3cret" roles="manager-gui"/>

What we need to do is edit this file and add this recommended role. Ordinarily, docker images don't have editors like
vi or nano installed by default. Instead of trying to add an editor to the image and editing the file in the container
I decided to copy the required file from the container to the host, edit it and then use that to overwrite the
original in the container. Here are the required steps:

Open a second terminal window as we need to first copy the **tomcat-users.xml** file from the container so
we can edit it.

Make a temporary directory to hold the file(s) we want to modify. In this example, I'll make an **extras** directory.

.. code:: bash

   mkdir extras

.. Warning::

   You can name this directory anything you want but be sure there's not a directory with the same name in the
   contain in the path where you plan to copy it

Copy the **tomcat-users.xml** file from its location in the Tomcat container to the **extras** directory you just
created on the host machine.

.. code:: bash

   docker cp Tomcat:/usr/local/tomcat/conf/tomcat-users.xml extras/tomcat-users.xml

   # With the file in ./conf/tomcat-users.xml on the host, edit the file and add the following:
   #   <role rolename="manager-gui"/>
   #   <user username="tomcat" password="sc00by" roles="manager-gui"/>

   nano conf/tomcat-users.xml

With the file updated, we need to save it back in the Tomcat container. We can do this by specifying a
volume that creates a new directory in the container

.. code:: bash

   docker run -it --rm -p 8888:8080 -v /home/hirosh7/extras/:/usr/local/tomcat/extras/ --name Tomcat tomcat:8.0

This command will create the Tomcat container again but add an **extras** directory under '/usr/local/tomcat/' which
is mapped to the **extras** directory on our host. Now you can log into the container to verify that both the **extras**
directory has been created and that our updated 'tomcat-users.xml' file is in it.

.. code:: bash

   docker exec -i -t Tomcat /bin/bash

**In the container**, copy the 'extras/tomcat-users.xml' to '/usr/local/conf/. By default, you'll be in the
'/usr/local/tomcat' directory when you log into the container.

.. code:: bash

   cp extras/tomcat-users.xml conf

At this point, the offical **tomcat-users.xml** is updated with our required change, so now we need to make the change
permanent. We can do this by committing this change into a new image.

.. Note::

   Any approach to this is to copy the file from the host to the container by just reversing the parameters to
   'docker cp'.

.. code:: bash

   # get the Tomcat container ID
   docker ps

   # Save our update to a new image
   docker commit <container_id>  <image_name> (e.g. secops_tomcat)

If you do run 'docker images' at this point, you'll see our new **secop_tomcat** image listed. Now we need to push it
up to Docker Hub so that we can use it on any machine. Details for this section are pulled from `here
<https://ropenscilabs.github.io/r-docker-tutorial/04-Dockerhub.html>`_

.. code:: bash

   # log into Docker Hub - it's recommended to use --password-stdin but I couldn't get that to work at the time
   docker login --username=<hub_username> --password=<hub_password>

   # Tag your image - here 'hirosh7' is my Docker Hub username
   docker tag <image_ID> hirosh7/secops_tomcat:latest

  # Push your image to Docker Hub
  docker push hirosh7/secops_tomcat:latest

.. Note::

  Pushing to Docker Hub is great, but it does have some disadvantages:

  * Bandwidth - many ISPs have much lower upload bandwidth than download bandwidth.
  * Unless you’re paying extra for the private repositories, pushing equals publishing.
  * When working on some clusters, each time you launch a job that uses a Docker container it pulls the container from
    Docker Hub, and if you are running many jobs, this can be really slow.

  Solutions to these problems can be to save the Docker container locally as a a tar archive, and then you can easily
  load that to an image when needed.

  To save a Docker image after you have pulled, committed or built it you use the docker save command. For example,
  let's save a local copy of the docker image we made:

  **docker save secops_tomcat > secops_tomcat.tar**

  If we want to load that Docker container from the archived tar file in the future, we can use the docker load
  command:

  **docker load --input secops_tomcat.tar**

Now we've saved our update image and pushed a copy to Docker Hub. Next we want to integrate all of this into our
**docker-compose.yaml** file. We'll need to specify the following parameters:

* Ports: 8888:8080 (we'll access Tomcat on localhost:8888)
* Container-name: Tomcat
* Image: hirosh7/secops_tomcat













