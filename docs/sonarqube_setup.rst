SonarQube Setup
===============
We'll also add SonarQube as a docker container so we'll need to update our original **docker-compose.yaml** file to
include the new SonarQube container service. As a reminder, our initial docker-compose.yaml file for our Gerrit service
looks like this:

.. code:: bash

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

We'll use the standard `SonarQube image <https://hub.docker.com/_/sonarqube/>`_ from Docker Hub.
Based on the instructions, it states that
**"By default, the image will use an embedded H2 database that is not suited for production"**. Although we're not
setting the sandbox up for production, since the H2 DB approach is also
not suitable for scaling nor for SonarQube upgrades (which we may want to do in our sandbox), we'll follow the details
in the **Database Configuration** section, particulary the link to `Github docker-sonarqube
<https://github.com/SonarSource/docker-sonarqube/blob/master/recipes.md>`_ which has a full SonarQube
docker-compose.yaml file. We'll splice that into our Gerrit docker-compose.yaml file and run both services from
there.

.. code:: bash

   new yaml file here


