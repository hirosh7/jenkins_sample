OWASP Dependency Check Integration
==================================
A good open source SAST tools is OWASP Dependency Check. It has good support in Jenkins via the OWASP
Dependency Check plugin which makes configuring it as part of your CI toolchain pretty simple. Details
for this section are derived from the article, `Checking vulnerabilities in 3rd party dependencies
using OWASP Dependency-Check Plugin in Jenkins
<https://medium.com/@PrakhashS/checking-vulnerabilities-in-3rd-party-dependencies-using-owasp-dependency-check-plugin-in-jenkins-bedfe8de6ba8>`_


Obviously, the first step is to go to the Jenkins dashboard, select Manage Jenkins->Manage Plugins
option and install the plugin. The installation process will install any related dependent plugins. With
the plugin installed, the setup has two parts


.. Note::

   These details are based on Jenkins Version 2.89.4

To get our feet wet with an initial Jenkins integration, we'll automate building a small Java webapp. The details for
this are pulled from `here
<https://jenkins.io/doc/tutorials/build-a-java-app-with-maven/>`_
