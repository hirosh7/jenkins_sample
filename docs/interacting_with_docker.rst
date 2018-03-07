Docker Overview
===============

Since what's actually created within the Kubernetes cluster pods are docker containers,
we should step back and get a better understanding of Docker. Data for this section was
pulled from `Docker for Beginners <https://docker-curriculum.com/>`_.

Helpful Docker Commands
---------------------------

drop knowledge here

.. code-block:: bash

   # Test docker installation
   docker run hello-world

   # List Docker Images
   docker images

  # Fetch an image from the docker registry
  docker pull <image_name>

  # Run a docker container based on a specified image
  # Note the --rm flag that can be passed to docker run which automatically
  # deletes the container once it's exited from. This helps with clean up
  docker run <image_name>

  # -d detach from terminal -P publish all exposed ports to random ports
  docker run -d -P --name <container_name> <image_name>

  # See ports a container is running on
  docker port <container_name>

  # Stop a detached container
  docker stop <container_ID>

  # Remove docker container
  docker rm <container_id>

  # Remove all docker containers with status 'exited'
  # -q parameter only returns the numeric IDs
  docker rm $(docker ps -a -q -f status=exited)

  # Remove docker image
  docker rmi <image_name>

  # Build a docker image
  # -t flag <optional_tag_name> (e.g. hirosh7/dogpark
  docker build -t <tag_name> .

  # Login to Docker to prepare for a push
  docker login

  # Push a new image to Docker Hub
  docker push <image_tag>

  # Attach to a running container
  docker exec -i -t <container_ID> /bin/bash #by ID
  docker exec -i -t <container_name> /bin/bash #by Name

  # Copy a file from a docker container to a host directory
  docker cp <container_name>:/foo /tmp/foo

  # Create a new docker image from changes made to the current image
  docker commit <container_id>  <image_name> (e.g. secops_tomcat)

  # To save a Docker image after you have pulled, committed or built it you use the docker save command. For example,
  # let's save a local copy of the docker image we made:
  docker save secops_tomcat > secops_tomcat.tar

  # If we want to load that Docker container from the archived tar file in the future, we can use the docker load
  # command:
  docker load --input secops_tomcat.tar







