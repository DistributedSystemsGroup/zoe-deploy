# Zoe Deploy
This repository explains how to install [zoe](https://github.com/DistributedSystemsGroup/zoe) by deployment scripts.

Installing Zoe
==============

Multiple deployment options are available:

* Demo install via Docker Compose
* Deployment scripts

Each is detailed in the following sections.

Docker compose - demo install
-----------------------------

In the repository there is a ``docker-compose.yml`` file that can be used to start a simple Zoe deployment for testing and demonstration purposes. By modifying the compose configuration file and adding volumes with customized configuration files it is possible to run more complex Zoe configurations.

Deployment Scripts
------------------

Deployment scripts are available for Linux or Windows machines:

* For Linux, we can deploy through bash script or Ansible playbook.
* For Windows, we deploy Zoe through Docker-Toolbox for Windows.

### Linux automated deployment
##### Swarm Deployment Scripts
* Overview

  - The following steps describe how to run a minimal workable Zoe on a fresh Ubuntu machine. The current supported OS is Ubuntu 16.04 but it is straightforward to modify to work with other versions.

* What will it do

  - Install docker
  - Create a Swarm cluster
  - Clone Zoe repository
  - Use docker-compose to get zoe-api, zoe-master and postgres up

* How to do it

  - We supports two kinds of deployment for Linux which is through bash script and ansible playbook.
  - For ansible playbook, we assume you are familiar with ansible and we leave the pre-setup at your side (ssh key, host name).

    - ``git clone http://github.com/DistributedSystemsGroup/zoe-deploy.git`` Then:

      - ``swarm/linux/bash`` folder, then ``chmod +x deploy.sh && ./deploy.sh`` or:

      - ``swarm/linux/ansible`` folder, modify the ``hosts`` file due to your system, then ``ansible-playbook -i hosts playbook.yml``

##### Kubernetes Deployment Scripts

* Overview

  - Currently, there are many ways to setup a Kubernetes cluster (kubeadm, kubernetes script, minikube).

    - For kubeadm, please refer to https://kubernetes.io/docs/getting-started-guides/kubeadm/

    - For kubernetes deploy scripts, please pick your OS and refer to: https://kubernetes.io/docs/getting-started-guides/#bare-metal

    - For minikube, please refer to https://kubernetes.io/docs/getting-started-guides/minikube/

  - For production, we suggest to setup manually Kubernetes on your premises. For developing, kubeadm and minikube could be used to quickly have a workable Kubernetes cluster.

* What will it do?

  - It creates three replication controllers

    - zoe-master

    - zoe-api

    - postgres

  - Link to those three replication controllers are three associated services.

* How to do it?

  - ``git clone http://github.com/DistributedSystemsGroup/zoe-deploy.git``

  - Go to ``kubernetes/linux`` then:

    - ``kubectl create -f zoe-postgres``

    - ``kubectl create -f zoe-api``

    - ``kubectl create -f zoe-master``

##### Kubernetes Helm Chart

* Overview

  - Helm is the kubernetes package manager, which is used to manage Kubernetes chart.
  - With current Zoe, we could deploy it via a Zoe Chart.
  - We assume that you have already had a workable Kubernetes cluster and Helm installed.

* What will it do?

  - From Helm, it creates three deployments:

    - zoe-master
    - zoe-api
    - zoe-postgres

  - Link to those three deployments are three associated services.

* How to do it?

  - ``git clone http://github.com/DistributedSystemsGroup/zoe-deploy.git``

  - Go to ``kubernetes/linux``, the configuration file is contained in ``zoe/values.yaml`` file, then:

    - ``helm install zoe``

### Windows automated deployment

* Overview

  - The following steps describe how to run a minimal workable Zoe on Windows machine using Docker Toolbox. The Windows machine has to meet the minimum requirement to run docker here https://docs.docker.com/toolbox/toolbox_install_windows/#step-1-check-your-version

* What will it do

  - Replace old profile from boot2docker with new profile to support creating a Swarm cluster
  - Create a Swarm cluster
  - Install docker-compose and get zoe-api, zoe-master, postgres up by using docker-compose

* How to do it

  - Go to https://docs.docker.com/toolbox/toolbox_install_windows/ to install docker-toolbox on your Windows machine
  - Open Docker Toolbox Terminal, then

    - ``git clone http://github.com/DistributedSystemsGroup/zoe-deploy.git`` then:
    -  Go to ``swarm/windows`` folder and ``chmod +x deploy.sh && ./deploy.sh``
