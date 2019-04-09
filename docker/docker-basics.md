# Overview of Docker
> Docker is an application that makes it simple and easy to run application processes in a container, which are like virtual machines, only more portable, more resource-friendly, and more dependent on the host operating system. For a detailed introduction to the different components of a Docker container, check out [The Docker Ecosystem: An Introduction to Common Components.](https://www.digitalocean.com/community/tutorials/the-docker-ecosystem-an-introduction-to-common-components "The docker official docs")

# Install Docker on CentOS 7
First, lets update our system packages to get the latest docker version from the official Docker repository.

```bash
#Check for any updates
$ sudo yum check-update

# Install the updates if available
$ sudo yum update -y
```

Run this command to add the official Docker repository, download the latest version of Docker and install it.

```bash
$ curl -fsSL https://get.docker.com/ | sh
```

After installation is complete, start the docker Daemon

```bash
$ sudo systemctl start docker

# Verify that it is running
$ sudo systemctl status docker
```

Lastly, make sure that docker is running at every reboot

```bash
$ sudo systemctl enable docker
```

# Basic Docker Commands

### CONTAINER COMMANDS.

```bash
# List all containers on the system
$ docker container ls -a

# List all the running containers on the system
$ docker container ls

# Short-hand for listing all containers 
$ docker ps -a

# Create and publish a container (Interactive mode)
$ docker container run -it -p 8080:80 nginx

# Create and publish a container (Detatch mode)
$ docker container run -d -p 8080:80 nginx

# Specify a custom name for the container
$ docker container run -it -p 8080:80 --name mynginx nginx

# Remove a container using either the id or name
$ docker container rm mynginx

$ docker container rm 9fca

# Stop a running container
$ docker container stop mynginx

# Force remove a running container (-f)
$ docker container rm mynginx -f

# Remove all containers (-f "To force remove running containers")
$ docker rm $(docker ps -aq) -f
```

* The __-it__ flag is to specify that we want to run the container on the iteractive mode.

* The __-p__ flag in full __--publish__ for publishing the container.

* The __-d__ flag in full __--detatch__ is to run the container in the background or detatch mode.


### IMAGE COMMANDS

```bash
# List out all the images on the system
$ docker images

# Pull an image from docker
$ docker pull httpd

# Delete an image using its ID
$ docker image rm dfc
```

### HOW TO ACCESS CONTAINERS
```bash
# Bash into an nginx environment
$ docker container exec -it mynginx bash

# Open the container in a text editor from the directory you are in.
$ docker container run -d -p 8080:80 -v $(pwd):/usr/share/nginx/html --name myng-website nginx

```

### CREATE AND PUBLISH IMAGES TO DOCKER-HUB

```bash
# Create an image on your system
$ docker image build -t petergich/nginx-trial .

# Create a container using the custom image we built out
$ docker container run -d -p 8082:80 petergich/nginx-trial

# Push the built image to docker hub
$ docker push petergich/nginx-trial
```