Setting Up Dockerized Gerrit
============================
We'll plan to run Gerrit from a docker container. We'll try working with the
`gerritcodereview/gerrit image <https://hub.docker.com/r/openfrontier/gerrit/>`_.
The documentation suggests to run with the following **docker-compose.yaml** file

.. code-block:: bash

    version: '3'

    services:
      gerrit:
        image: gerritcodereview/gerrit
      volumes:
         - git-volume:/var/gerrit/git
         - db-volume:/var/gerrit/db
         - index-volume:/var/gerrit/index
         - cache-volume:/var/gerrit/cache
      ports:
         - "29418:29418"
         - "8081:8080"

    volumes:
      git-volume:
      db-volume:
      index-volume:
      cache-volume:

This approach will set up local persistent volumes. Then to kick this off, just run

.. code-block:: bash

   docker-compose up

.. Note::
   Since we already have our local Jenkins server running on port 8080 we need to configure the Gerrit docker
   container to use a different port. So in the **docker-compose.yaml** file we want to specify a different port mapping.
   Per the `docker run man page
   <https://docs.docker.com/engine/reference/commandline/run/#add-bind-mounts-or-volumes-using-the-mount-flag>`_, the port
   mapping is <host machine port>:<container port>. So, if you have a port mapping like
   **8081:8080**, messages routed to port **8081** on the host machine will hit the container port 8080. This is what
   we want. So we'll use the following **docker run** command instead:

**Todo: figure out how to look at detached container logs!**


