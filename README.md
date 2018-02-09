# docker-ansible

## Description

This repository contains several Dockerfiles, each one used for building an Ansible Docker image using a different mechanism.

* [Dockerfile-apk](./Dockerfile-apk)
  * Uses Alpine Linux apk package management tool for installing Ansible
  * Ansible packages can be found [here](https://pkgs.alpinelinux.org/packages?name=ansible&branch=v3.6)
  * Pros
    * Rather small ~ 97MB
  * Cons
    * Unable to run Ansible latest & greatest, since it's limited to the published apk Ansible packages
* [Dockerfile-pip](./Dockerfile-pip)
    * Uses Python pip package management tool for installing Ansible
    * Ansible packages can be found [here](https://pypi.python.org/pypi/ansible)
    * Pros
      * Small(ish) ~ 260MB
      * Able to run (almost) all available Ansible versions
    * Cons
      * Might not be able to run Ansible latest & greatest, since it's limited to the published pip Ansible packages

## Dockerfile-apk

### Build Docker image

````bash
docker image build \
       --file Dockerfile-apk \
       --tag satrapu/ansible-alpine-apk:2.3.1.0-r0 \
       --tag satrapu/ansible-alpine-apk:latest \
       .
````

### Publish Docker image to Docker Hub

````bash
docker image push satrapu/ansible-alpine-apk:2.3.1.0-r0
docker image push satrapu/ansible-alpine-apk:latest
````

### Image @ Docker Hub
https://hub.docker.com/r/satrapu/ansible-alpine-apk

### Run Docker container

````bash
docker container run \
       --rm -it \
       -v <DOCKER_HOST_ANSIBLE_PLAYBOOK_HOME>:/opt/ansible-playbooks \
       satrapu/ansible-alpine-apk \
       ansible-playbook <ANSIBLE_PLAYBOOK>
````

Example (ConEmu PowerShell tab; Docker version 17.06.0-ce, build 02c1d87; Windows 10 Pro, version 1703)

<code lang="powershell">
docker container run --rm -it -v D:\\Satrapu\\Ansible:/opt/ansible-playbooks satrapu/ansible-alpine-apk ansible-playbook ./hello-world/hello-world.yml<sup><a href="#hello-world-yml">1</a><sup>
</code>

## Dockerfile-pip

### Build Docker image

````bash
docker image build \
       --file Dockerfile-pip \
       --tag satrapu/ansible-alpine-pip:2.3.1.0 \
       --tag satrapu/ansible-alpine-pip:latest \
       .
````

### Publish Docker image to Docker Hub

````bash
docker image push satrapu/ansible-alpine-pip:2.3.1.0
docker image push satrapu/ansible-alpine-pip:latest
````

### Image @ Docker Hub
https://hub.docker.com/r/satrapu/ansible-alpine-pip

### Run Docker container

````bash
docker container run \
       --rm -it \
       -v <DOCKER_HOST_ANSIBLE_PLAYBOOK_HOME>:/opt/ansible-playbooks \
       satrapu/ansible-alpine-pip \
       ansible-playbook <ANSIBLE_PLAYBOOK>
````

Example (ConEmu PowerShell tab; Docker version 17.06.0-ce, build 02c1d87; Windows 10 Pro, version 1703)

<code lang="powershell">
docker container run --rm -it -v D:\\Satrapu\\Ansible:/opt/ansible-playbooks satrapu/ansible-alpine-pip ansible-playbook ./hello-world/hello-world.yml<sup><a href="#hello-world-yml">1</a><sup>
</code>

---
<a name="hello-world-yml">1</a> The Ansible playbook **hello-world.yml** can be found [here](https://gist.github.com/satrapu/31b1a03f321990f8d9ae067372a8b456).
