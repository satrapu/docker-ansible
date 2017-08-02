# docker-ansible

## Description

This repository contain several Dockerfile, each one used for building Ansible Docker images.

* Dockerfile-apk
  * Uses Alpine Linux apk package management tool for installing Ansible
  * Ansible packages can be found [here](https://pkgs.alpinelinux.org/packages?name=ansible&branch=v3.6)
  * Pros
    * Rather small ~ 84MB
  * Cons
    * Unable to run Ansible latest & greatest, since it's limited to the published apk Ansible packages
* Dockerfile-pip
    * Uses Python pip package management tool for installing Ansible
    * Ansible packages can be found [here](https://pypi.python.org/pypi/ansible)
    * Pros
      * Not that small ~ 250MB
      * Able to run (almost) all available Ansible versions
    * Cons
      * Unable to run Ansible latest & greatest, since it's limited to the published apk Ansible packages

## Dockerfile-apk

### Build Docker image

````bash
docker image build --file Dockerfile-apk --tag ansible-alpine-apk:2.3.1.0-r0 --tag ansible-alpine-apk:latest .
````

### Run Docker container

````bash
 docker container run --rm -it -v <DOCKER_HOST_ANSIBLE_PLAYBOOK_HOME>:/opt/ansible-playbooks ansible-alpine-apk ansible-playbook <ANSIBLE_PLAYBOOK>
````

## Dockerfile-pip

### Build Docker image

````bash
docker image build --file Dockerfile-pip --tag ansible-alpine-pip:2.3.1.0 --tag ansible-alpine-pip:latest .
````

### Run Docker container

````bash
 docker container run --rm -it -v <DOCKER_HOST_ANSIBLE_PLAYBOOK_HOME>:/opt/ansible-playbooks ansible-alpine-pip ansible-playbook <ANSIBLE_PLAYBOOK>
````