Tomcat Setup
============
We'll also install Tomcat in a docker container. Some configuration files will need to be changed so we'll start with
the `base Tomcat image <https://hub.docker.com/_/tomcat/>`_ from Docker Hub. Initially we'll just start it up in
interactive mode.

.. code:: bash

   docker run -it --rm -p 8888:8080 tomcat:8.0

Now open a second terminal window as we need to first copy the **tomcat-users.xml** file from the container so
we can edit it.

.. code:: bash

   # get the tomcat name
   docker ps

   # copy the tomcat-users.xml file from its location in the Tomcat container to the 'conf' directory on
   # the host machine. This assumes you have already created a 'conf' directory where you are executing
   # the 'docker cp command
   docker cp <container_name>:/usr/local/tomcat/conf/tomcat-users.xml conf/tomcat-users.xm


