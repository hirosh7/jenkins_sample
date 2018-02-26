Setting Up Dockerized Gerrit
============================
We'll plan to run Gerrit from a docker container. We'll try working with the most
popular image on Docker Hub, `openfrontier/gerrit <https://hub.docker.com/r/openfrontier/gerrit/>`_.
Based on the documentation there, all you should have to do is run

.. code-block:: bash

   docker run -d -v ~/gerrit_volume:/var/gerrit/review_site -p 8080:8080 -p 29418:29418 openfrontier/gerrit

But since we already have our local Jenkins server running on port 8080 we need to configure the Gerrit docker
container to use a different port. So in the **docker run** command line we want to specify a different port mapping.
Per the `docker run man page
<https://docs.docker.com/engine/reference/commandline/run/#add-bind-mounts-or-volumes-using-the-mount-flag>`_, the port
mapping behind the **-p** option is <host machine port>:<container port>. So, if you have a port mapping like
**8081:8080**, messages routed to port **8081** on the host machine will hit the container port 8080. This is what
we want. So we'll use the following **docker run** command instead:

.. code-block:: bash

   mkdir ~/gerrit_volume
   docker run -d -v ~/gerrit_volume:/var/gerrit/review_site -p 8080:8080 -p 29418:29418 openfrontier/gerrit

This will set Gerrit up to run detached and use **~/gerrit_volume** as the Gerrit local site storage.

**Todo: figure out how to look at detached container logs!**


