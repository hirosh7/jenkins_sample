Adding a Jenkins Agent
======================

1. Ensure a java version is installed on the agent **before** proceeding to the the Jenkins agent configuration
   and connection step. I used `this reference
   <http://tipsonubuntu.com/2016/07/31/install-oracle-java-8-9-ubuntu-16-04-linux-mint-18/>`_ to configure
   java on my Ubuntu agent server (sokovia).

2. Ensure that Git is installed on the agent **before** proceeding to the Jenkins agent configuration and
   connection step.

3. Ensure that Docker is installed on the agent **before** proceeding to the Jenkins agent configuration and
   connection step.

   - needs more configuring: https://devopscube.com/docker-containers-as-build-slaves-jenkins/

2. For configuring and connecting the Jenkins agent I used `How to connect to remote agents
   <https://support.cloudbees.com/hc/en-us/articles/222978868-How-to-Connect-to-Remote-SSH-Agents->`_

You might want to add an ansible playbook for configuring agent with Java. This would be a good practice exercise.
Steps would be:

* Confirm if Java is installed on the agent (adhoc command) ('java -version')

  * If not, code up the steps in the Java install reference above

* Confirm if Git is installed on the agent (adhoc command) ('git --version')

  - If not, code up a simple install (sudo apt install git)

* Confirm if Docker is installed on the agent (adhoc command) ('/snap/bin/docker --version')

  - If not, code up a simple install (sudo snap install docker)


