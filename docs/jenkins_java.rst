Jenkins Java Webapp Automation
==============================

.. Note::

   These details are based on Jenkins Version 2.89.4

To get our feet wet with an initial Jenkins integration, we'll automate building a small Java webapp. The details for
this are pulled from `here
<https://jenkins.io/doc/tutorials/build-a-java-app-with-maven/>`_

Fork The Sample Application
---------------------------

The Jenkins docker should already be set up if you've followed the directions in **Jenkins Setup (Dockerized Container)
section**. I started on the **Fork and clone the sample repository on GitHub** section.
This is simple enough. Just log into GitHub, click on the repo link and click the 'Fork' button. GitHub will then
place a copy of the repo under your account. With this, our test source code repo is set up and our repo URL is
**https://github.com/hirosh7/hello-world-servlet***. Below this referred to as our **'forked GitHub repository'**.

Create your Pipeline project in Jenkins
---------------------------------------
1) Go back to Jenkins, log in again if necessary and click create new jobs under Welcome to Jenkins!

   * **Note: If you don’t see this, click New Item at the top left.**

2) In the Enter an item name field, specify the name for your new Pipeline project (e.g. simple-java-maven-app).
3) Scroll down and click Pipeline, then click OK at the end of the page.

   * ( Optional ) On the next page, specify a brief description for your Pipeline in the Description
     field (e.g. An entry-level Pipeline demonstrating how to use Jenkins to build a simple Java application
     with Maven.)

4) Click the Pipeline tab at the top of the page to scroll down to the Pipeline section.
5) From the **Definition** field, choose the **Pipeline script from SCM option**. This option instructs Jenkins
   to obtain    your Pipeline from Source Control Management (SCM), which will be your forked Github repository.
6) From the **SCM** field, choose **Git**.
7) In the **Repository URL** field, specify the directory path of your forked Github repository above

   * Note: You can also do this from a local directory since we've mapped to the /home directory of the Jenkins
     container

8) This example app includes a complete **Jenkinsfile** that executes 'build', 'test', and 'deliver' stages. However,
   in the dialog, you need to update the **'Script Path'**. It defaults to 'Jenkinsfile' but note in the sample app
   directory structure, the Jenkinsfile is actually located in the **jenkins** folder so the correct path is
   **'jenkins/Jenkinsfile'**.
