Jenkins Java Webapp Automation
==============================
.. Note::

   These details are based on Jenkins Version 2.89.4

To get our feet wet with an initial Jenkins integration, we'll automate building a small Java webapp. The details for
this are pulled from `here
<https://www.javaworld.com/article/3123117/development-tools/open-source-java-projects-jenkins-with-docker-part-1.html>`_

This article is a little dated but gets the basics well enough to succeed with the goal. Here are the details with
my corrections starting at the section titled, 'Jenkins CI for a Java web app'.

The first thing I did was fork a copy of the author's sample `hello-world-servlet
<https://github.com/ligado/hello-world-servlet>`_ on GitHub. This is simple enough. Just log into GitHub, click
on the repo link and click the 'Fork' button. GitHub will then place a copy of the repo under your account. So
now our test source code repo is set up.

Configure Jenkins Global Tools
------------------------------

Now on the Jenkins Dashboard (i.e. top level Jenkins page):

* Click **Manage Jenkins**

  * Choose **Global Tool Configuration**
  * First configure a JDK. Under the JDK section:

    * Click **Add JDK** and give it a name (e.g. OpenJDK 8)
    * Specify the JAVA_HOME path. Here's it's **'/usr/lib/jvm/java-8-openjdk-amd64/'**. You can find this path by
      running **'> update-java-alternatives --list'** on the command line

  * Configure Git similarly
  * Configure Maven

    * Click **Add Maven** and give it a name (e.g. Maven 3.5.0)
    * Specify the MAVEN_HOME path. You can find this along with the version by running **'mvn --version'** on
      the command line

  * Configure Docker

    * Click **Add Docker** and give it a name
    * If you leave the **'Installation root'** blank, Jenkins will go with the default install root path

  * Click **'Save'**

.. image:: images/jenkins-config-jdk-git.png
   :align: center


.. image:: images/jenkins-config-mnv-docker.png
   :align: center

At this point, Jenkins knows where all the tools are required for the following steps. We really aren't using
Docker in this exercise, but it's good to get it out of the way.

Configure Jenkins Build Job
---------------------------

Now back on Jenkins Dashboard:

* Click the **New Item** button and enter the name of your project (e.g. hello-world-servlet)
* Choose the **Freestyle Project** project type
* Click **Ok**

This will take you to the job configuration page below similar to the figure below.

.. image:: images/jenkins-create-job.png
   :align: center

* Choose 'GitHub project'
* Enter the GitHub URL of your project (e.g. https://github.com/hirosh7/hello-world-servlet)
* Under **Source Code Management**:

  * Choose 'Git'
  * Enter the same project URL (e.g. https://github.com/hirosh7/hello-world-servlet)

* The article referenced a **Build when a change is pushed to GitHub** option which is not there in the latest
  this version of Jenkins so I didn't select anything in the **Build Triggers** section. The idea is to choose
  an option so that Jenkins will build your code anytime you push a change to GitHub but obviously this is now
  configured differently

* In the **Build** section, add a new build step, choose **Invoke top-level Maven targets**:

  * Choose the Maven instance that you configured previously (such as "Maven 3.3.9")
  * Enter 'clean install' in the goals field

.. image:: images/jenkins-create-job-2.png
   :align: center

We'll also configure Jenkins to generate a report that summarizes the unit test execution

* Click **Add post-build action**
* Choose **Publish JUnit test result report**
* Enter the following in the **Test Reports XMLs** text field:

.. code:: bash

   **/target/surefire-reports/*.xml

* When you're finished, press **Save**

The **Test Reports XMLs** field points to the directory where your Surefire tests are published.
Maven creates a target directory, a surefire-reports subdirectory, and then publishes a set of XML files
summarizing the test results to the new directory.

.. image:: images/jenkins-post-build-actions.png
   :align: center

Running the Job
---------------
Okay, finally ready to have Jenkins run a build! Back on the Jenkins Dashboard, you should now see your
job listed similar to the image below.

.. image:: images/jenkins-dashboard-with-job.png
   :align: center

Click on the **'Build'** icon (highlighted in red). Assuming the build was successful, you'll see a little build
number under the **'Last Success'** column (e.g. #1). It's a link, so you can click on it to get to the build
details screen. To check out the build output, click on **'Console Output'** option in the left nav bar. At the
bottom of the build details screen you'll also see a link for **'Test Results'**. This will, obviously, show
you the results of any unit tests run.


