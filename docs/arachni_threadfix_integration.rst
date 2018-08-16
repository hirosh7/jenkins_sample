Arachni and Threadfix Integration
=================================
There is a good, high-level
`article <https://blog.secodis.com/2016/03/17/automated-security-tests-3-jenkins-arachni-threadfix/>`_
(albeit a bit dated) on integrating the open source DAST tool,
Arachni into your CI environment along with ThreadFix - a web-based tool for collecting
findings from different tools such as Arachni. Let's give that a whirl.


https://wiki.jenkins.io/display/JENKINS/Deploy+Plugin
install plugin via Jenkins Plugin Manager

New approach:
use one agent to build and stash artifact to a directory
in a test stage, use another agent (tomcat docker container) to pick up war file
via volumes mounts e.g. /build_stach_dir:/usr/local/tomcat/webapps)
invoke arachni on that URL

curl --upload-file target/JSPWiki.war "http://jenkins:Dutchy7@localhost:8888/manager/text/deploy?path=/JSPWiki&update=true"
