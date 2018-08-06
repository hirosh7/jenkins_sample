OWASP Dependency Check Integration
==================================
A good open source SAST tools is OWASP Dependency Check. It has good support in Jenkins via the OWASP
Dependency Check plugin which makes configuring it as part of your CI toolchain pretty simple. Details
for this section are derived from the article, `Checking vulnerabilities in 3rd party dependencies
using OWASP Dependency-Check Plugin in Jenkins
<https://medium.com/@PrakhashS/checking-vulnerabilities-in-3rd-party-dependencies-using-owasp-dependency-check-plugin-in-jenkins-bedfe8de6ba8>`_


Obviously, the first step is to go to the Jenkins dashboard, select Manage Jenkins->Manage Plugins
option and install `the plugin <https://wiki.jenkins.io/display/JENKINS/GitHub+Plugin>`_.
The installation process will install any related dependent plugins. With the plugin installed,
the setup has two parts:

* Setting up a Jenkins job to cache the National Vulnerability Database (NVD) vulnerability data
* Adding a new stage to your Jenkinsfile to run OWASP DC on your project

Both steps are well defined in the first reference link mentioned above and won't be repeated here. It's
a straightforward set up.
