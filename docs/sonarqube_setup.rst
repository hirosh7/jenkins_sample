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
      sonarqube:
          image: sonarqube
          ports:
            - "9000:9000"
          networks:
            - sonarnet
          environment:
            - SONARQUBE_JDBC_URL=jdbc:postgresql://db:5432/sonar
          volumes:
            - sonarqube_conf:/opt/sonarqube/conf
            - sonarqube_data:/opt/sonarqube/data
            - sonarqube_extensions:/opt/sonarqube/extensions
            - sonarqube_bundled-plugins:/opt/sonarqube/lib/bundled-plugins

      db:
        image: postgres
        networks:
          - sonarnet
        environment:
          - POSTGRES_USER=sonar
          - POSTGRES_PASSWORD=sonar
        volumes:
          - postgresql:/var/lib/postgresql
          # This needs explicit mapping due to
          # https://github.com/docker-library/postgres/blob/4e48e3228a30763913ece952c611e5e9b95c8759/Dockerfile.template#L52
          - postgresql_data:/var/lib/postgresql/data

    networks:
      sonarnet:
        driver: bridge

    volumes:
      # SonarQube Volumes
      sonarqube_conf:
      sonarqube_data:
      sonarqube_extensions:
      sonarqube_bundled-plugins:

      # PostgreSQL volumes
      postgresql:
      postgresql_data:

      # Gerrit Volumes
      git-volume:
      db-volume:
      index-volume:
      cache-volume:

The new configuration is now running three containers - Gerrit, SonarQube and a PostgreSQL DB.

.. code:: bash

    docker-compose ps

           Name                      Command               State                        Ports
    ---------------------------------------------------------------------------------------------------------------
    hirosh7_db_1          docker-entrypoint.sh postgres    Up      5432/tcp
    hirosh7_gerrit_1      /bin/sh -c /var/gerrit/bin ...   Up      0.0.0.0:29418->29418/tcp, 0.0.0.0:8081->8080/tcp
    hirosh7_sonarqube_1   ./bin/run.sh                     Up      0.0.0.0:9000->9000/tcp

At this point, it looks like SonarQube has been successfully installed.

.. Note::
   Since the SonarQube installation also depends on the PostgreSQL DB, details on this docker image can be found
   `here <https://hub.docker.com/_/postgres/>`_



