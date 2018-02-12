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
* [Dockerfile-git](./Dockerfile-git)
    * Uses the Ansible sources hosted on GitHub for installing Ansible
    * Ansible sources can be found [here](https://github.com/ansible/ansible)
    * Pros
      * Large ~ 490MB
      * Able to run any Ansible commit
    * Cons
      * Its size
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

````powershell
docker image build --file Dockerfile-apk --tag satrapu/ansible-alpine-apk:2.4.1.0-r0 --tag satrapu/ansible-alpine-apk:latest .
````

### Publish Docker image to Docker Hub

````powershell
docker image push satrapu/ansible-alpine-apk:2.4.1.0-r0
docker image push satrapu/ansible-alpine-apk:latest
````

### Image @ Docker Hub
https://hub.docker.com/r/satrapu/ansible-alpine-apk

### Run Docker container

````powershell
docker container run --rm -v <DOCKER_HOST_ANSIBLE_PLAYBOOK_HOME>:/opt/ansible-playbooks satrapu/ansible-alpine-apk:latest ansible-playbook <ANSIBLE_PLAYBOOK>
````

Example (ConEmu PowerShell tab; Docker version 17.06.0-ce, build 02c1d87; Windows 10 Pro, version 1703)

<code lang="powershell">
docker container run --rm -v D:\\Satrapu\\Ansible:/opt/ansible-playbooks satrapu/ansible-alpine-apk ansible-playbook ./hello-world/hello-world.yml<sup><a href="#hello-world-yml">1</a><sup>
</code>

## Dockerfile-git

### Build Docker image

````powershell
docker image build --file Dockerfile-git --tag satrapu/ansible-alpine-git:devel-39d9496 --tag satrapu/ansible-alpine-git:latest --build-arg ANSIBLE_GIT_CHECKOUT_ARGS=39d9496 .
````

### Publish Docker image to Docker Hub

````powershell
docker image push satrapu/ansible-alpine-git:devel-39d9496
docker image push satrapu/ansible-alpine-git:latest
````

### Image @ Docker Hub
https://hub.docker.com/r/satrapu/ansible-alpine-git

### Run Docker container

````powershell
docker container run --rm -v <DOCKER_HOST_ANSIBLE_PLAYBOOK_HOME>:/opt/ansible-playbooks satrapu/ansible-alpine-git:latest ansible-playbook <ANSIBLE_PLAYBOOK>
````

Example (ConEmu PowerShell tab; Docker version 17.06.0-ce, build 02c1d87; Windows 10 Pro, version 1703)

<code lang="powershell">
docker container run --rm -v D:\\Satrapu\\Ansible:/opt/ansible-playbooks satrapu/ansible-alpine-git ansible-playbook ./hello-world/hello-world.yml<sup><a href="#hello-world-yml">1</a><sup>
</code>

## Dockerfile-pip

### Build Docker image

````powershell
docker image build --file Dockerfile-pip --tag satrapu/ansible-alpine-pip:2.5.0b1 --tag satrapu/ansible-alpine-pip:latest .
````

### Publish Docker image to Docker Hub

````bash
docker image push satrapu/ansible-alpine-pip:2.5.0b1
docker image push satrapu/ansible-alpine-pip:latest
````

### Image @ Docker Hub
https://hub.docker.com/r/satrapu/ansible-alpine-pip

### Run Docker container

````powershell
docker container run -v <DOCKER_HOST_ANSIBLE_PLAYBOOK_HOME>:/opt/ansible-playbooks satrapu/ansible-alpine-pip:latest ansible-playbook <ANSIBLE_PLAYBOOK>
````

Example (ConEmu PowerShell tab; Docker version 17.06.0-ce, build 02c1d87; Windows 10 Pro, version 1703)

<code lang="powershell">
docker container run --rm -v D:\\Satrapu\\Ansible:/opt/ansible-playbooks satrapu/ansible-alpine-pip:latest ansible-playbook ./hello-world/hello-world.yml<sup><a href="#hello-world-yml">1</a><sup>
</code>

---
<a name="hello-world-yml">1</a> The Ansible playbook **hello-world.yml** can be found [here](https://gist.github.com/satrapu/31b1a03f321990f8d9ae067372a8b456).
