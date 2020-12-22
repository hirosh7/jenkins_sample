Helm/Kubernetes
===============

.. note::
   Last state mirror of stable charts and incubator charts will be moved to
   https://charts.helm.sh/stable and https://charts.helm.sh/incubator accordingly.

Standard Installation
*********************

.. code:: bash

   # Get latest release from https://github.com/helm/helm/releases
   $ wget https://get.helm.sh/helm-v3.4.2-linux-amd64.tar.gz

   # Extract
   $ tar -zxvf helm-v3.4.2-linux-amd64.tar.gz

   # Move helm to a central location
   $ mv linux-amd64/helm /usr/local/bin/helm

Snap Installation
*****************

.. code:: bash

   # Install Helm3 in the MicroK8S environment - not yet sure which one is the right one
   $ sudo snap install helm3 or sudo snap install helm3 latest/candidate
   $ microk8s enable helm3

   # Install a specific version. By default, Snap will install the version associated with the
   # latest/stable channel which is normally a much older version.
   $ snap install helm3 --channel=latest/candidate

   # Set up the config file
   $ microk8s.kubectl config view --raw > $HOME/.kube/config
   $ chmod 400 HOME/.kube/config

   # Uninstall Helm3
   $ sudo snap remove helm3

Useful Commands
***************

.. note::
   These notes are based on **helm3**. You can alias the 'helm3' command to just 'helm' for
   convenience but you need to remember that on some systems 'helm' indicates that you're using
   Helm version 2

.. code:: bash

   # Get Helm version info
   $ helm version

   # List all available packages on ArtifactHUB
   $ helm search hub

   # Search for a specific helm chart
   $ helm search hub mysql

   # Adding a helm repo
   $ helm repo add stable https://charts.helm.sh/stable

   # Remove a helm repo
   $ helm repo remove stable

   # List available repos
   $ helm repo list

   # Search repo
   $ helm search repo stable

   # Search repo for a specific chart
   $ helm3 search repo stable/mysql

   # Update a repo
   $ helm repo update

   # Install a helm chart. This example specifies a local name 'myairflow' and the chart name
   $ helm install myairflow stable/airflow

   # This version installs the chart and lets k8s generate a name for it
   $ helm install stable/airflow --generate-name

   # List installed charts
   $ helm ls

   # Delete an installed charts
   $ helm uninstall myairflow

   # Delete a K8S deployment (-n [namespace]). This example deletes an nginx deployment from
   # the 'default' namespace
   $ kubectl delete -n default deployment nginx

   # Create your own chart. Example here is 'mychart'
   $ helm create mychart


Miscellaneous
*************

Udemy Helm/Kubernetes course section on `Creating Chart Templates
<https://www.udemy.com/course/helm-package-manager-for-kubernetes-complete-
master-course/learn/lecture/20424933#overview>`_

.. code:: bash

   # Delete a Pod - in this case the 'ubuntu' pod from the 'default' namespace
   $ delete -n default pod ubuntu

   # Get K8S cluster info
   $ kb cluster-info

   # Search for a configmap
   $ kubectl describe configmaps <configmap_name>

   # Install a configmap. Example uses a the configmap.yaml file in folder mychart
   $ helm install helm-demo-configmap ./mychart




Troubleshooting
***************
Error: Kubernetes cluster unreachable
+++++++++++++++++++++++++++++++++++++
Try this from `How to make microk8s work with helm 3
<https://worklifenotes.com/2020/01/22/how-to-make-microk8s-work-with-helm/>`_

.. image:: images/mk8s_helm_workaround.png

.. important::
   Make sure to change the **microk8s.conf** file permissions to 400 to avoid warnings
















