Setting Up Dockerized Gerrit
============================
We'll plan to run Gerrit from a docker container. We'll try working with the
`gerritcodereview/gerrit image <https://hub.docker.com/r/openfrontier/gerrit/>`_.
The documentation suggests **docker-compose.yaml** file, but it should be updated to look like the following:

.. code-block:: bash

   version: "2"

   services:
     gerrit:
       image: gerritcodereview/gerrit
       ports:
         - "29418:29418"
         - "8081:8080"
       volumes:
         - git-volume:/var/gerrit/git
         - db-volume:/var/gerrit/db
         - index-volume:/var/gerrit/index
         - cache-volume:/var/gerrit/cache

   volumes:
     git-volume:
     db-volume:
     index-volume:
     cache-volume:


This approach will set up local persistent volumes. Then to kick this off, just run

.. code-block:: bash

   # Run docker-compose and detach all the containers from the terminal
   docker-compose up -d

.. Note::
   Since we already have our local Jenkins server running on port 8080 we need to configure the Gerrit docker
   container to use a different port. So in the **docker-compose.yaml** file we want to specify a different port mapping.
   Per the `docker run man page
   <https://docs.docker.com/engine/reference/commandline/run/#add-bind-mounts-or-volumes-using-the-mount-flag>`_, the port
   mapping is <host machine port>:<container port>. So, if you have a port mapping like
   **8081:8080**, messages routed to port **8081** on the host machine will hit the container port 8080. This is what
   we want. So note the update in the above file sample

In order to view the container logs (assuming you are running the container in detached mode), you can use the following
commands:

.. code-block:: bash

   # list the docker container IDs
   docker ps

   # check the container logs
   docker logs [option] <container ID>

   Options:
   --no-color          Produce monochrome output.
   -f, --follow        Follow log output
   -t, --timestamps    Show timestamps
   --tail="all"        Number of lines to show from the end of the logs
                       for each container.

