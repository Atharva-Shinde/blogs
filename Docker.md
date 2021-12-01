

#### What is Docker?
Docker is a platform that allows developers to containerise, build, test, deploy, ship applications much faster within multiple workspaces and making it ready for production deployments. Docker wraps your application inside an abstraction called container which helps in making your development workflow quick and easier.

#### Why Docker?
Docker streamlines the development processes by letting developers have control over managing, scaling and building applications. Docker being lightweight and portable makes it a cost-effective alternative to hypervisor virtual machines.
![Docker and hypervisors](https://www.docker.com/sites/default/files/d8/2018-11/docker-containerized-and-vm-transparent-bg.png)
With its simple CLI commands we can easily build, delete, deploy and manage containerised images on our machines. Moreover these containers are highly portable which enables them to be able to run on local systems, virtual machines, cloud providers or even in hybrid workspaces without worrying about setting up libraries and all other configuration files.
So if you need fast, lightweight, efficient and orchestrated way to run, scale, deploy or test your application/software on one or more virtualised/physical systems, Docker is your solution.


#### Docker Architecture
![Docker Architecture](https://docs.docker.com/engine/images/architecture.svg)

Docker implements Client-Server architecture. So what is Client-Server architecture? Consider online shopping. You (the client) orders a product from app-store and the service-provider (server) places the order, takes necessary actions and ships it to your address. Similarly a client-server architecture is an architecture where the client requests a service (in this case through Docker CLI) and the service provider (in this case Docker daemon) works on the request and provides desired result.
Referring the above diagram, if user wants to create a container from one of the installed images and therefore enters `docker run` command, docker daemon responds to the request and gives user a configured virtualised container along with its metadata.

### What is Docker Daemon?
Daemon is a program that runs consistently in the background which responds to particular request or action, and is not under any direct control of user, that means user cannot change the nature of the program. Usually daemon files/processes names are suffixed by 'd', for example:- *sshd, mysqld, dockerd.*
![Docker Workflow](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.oreilly.com%2Flibrary%2Fview%2Fcontinuous-delivery-with%2F9781787125230%2Fassets%2Fcadc3363-6814-489b-a770-58dd9ead6f56.png&f=1&nofb=1)
Docker Daemon listens to Docker Client through API requests and manages docker objects like images, containers, volumes, network.

#### Docker Client
Docker client is the primary way to interact with Docker. When we run a Docker command through terminal, the client sends the request to Docker Daemon which is responsible for managing commands.

### Docker Image
Docker Image is built of read-only stacked layers generated from instructions inside the image's dockerfile. Each layer is a representation of an instruction from the dockerfile. Images that are pre-built by developers and are available inside Container-Registries, a place to store and download images. One such popular public registry is DockerHub. Few companies also have private registries to store their images.

```
# to install an image in your system
docker pull <image-name:version>
# example docker pull ubuntu:20.04

# to see if the image is installed
docker image ls
# or
docker images

# to remove an image 
docker image rm <image-name or image-id>
# if you get an error message similar to daemon: conflict: unable to delete, then you must delete the container first
read more about containers below 

# to check layers of an image
docker image inspect <image-name or image-id>
```

### Dockerfile
To build your customised docker image create a Dockerfile with the extension `.dockerfile`. A new image layer is stacked for an instruction you define inside Dockerfile, but not every instruction is responsible for creating a layer.

Following is an example of dockerfile
```
# this is a comment
FROM ubuntu:18.04
LABEL org.opencontainers.image.authors="org@example.com"
COPY . /app
RUN make /app
RUN rm -r $HOME/.cache
CMD python /app/app.py
```

### .dockignore
If you have worked with GitHub before you may have used .gitignore file to exclude .env variables, dependency-directories, temporary files etc. Similarly for Docker we have `.dockignore` file to exclude files that are not relevant to the build.
Before a request from docker clients CLI reaches docker daemon it goes through `.dockignore` file and checks whether there is a context that needs to be excluded before passing to the daemon and thus preventing any large or sensitive information from reaching daemon.

### Docker Containers
Containers are isolated processes which run on a single host machine. Containers consists of packages and dependencies required by your application to run on your system. We can create, start, stop, delete, move and modify containers which is performed inside a thin writable layer know as 'Container Layer' built on top of immutable, read-only image layers. Containers therefore are running instances of an image. Each container has its own binaries, dependencies, and container-layer therefore each container being an isolated process make them fast, light-weight and more efficient to work with.
Below is an example of Image layers structure-
![Image structure](https://docs.docker.com/storage/storagedriver/images/container-layers.jpg)
P.S- If user downloads two or more version of the same image, docker only builds the layers which are new from previous versions and all the layers which are mutual won't be installed again.

```
# to build a container from installed image
docker run <image-name:version>

# to get list of all running containers metadata
docker ps 

# to get list of all containers metadata
docker ps -a

# to stop a container
docker stop <container-name or container-id>

# to restart a container
docker start <container-name or container-id>

# to remove a container 
docker container rm <container-name or container-id>

# to rename a container
docker stop <container-name or container-id>
docker run --name <your desired container-name> <image-name>

# to navigate inside a container's terminal
docker exec -it <container id or container name> /bin/bash
```

Containers helps in setting up environment on any OS without worrying about configurations and dependencies, and actually focusing on building applications.

So what's the catch? 
Containers are not persistent. Container when deleted or restarted, loses all its data and starts again from its image definition. So when we delete/restart a container the data inside 'container-layer' is lost and it starts from a fresh state. Now if we try to install/restart it again, the container layer is created from scratch not having any history of operations we did inside previous one. How do we solve this? 

### Persistent data
Persisting database is the solution to the above conflict. The idea is to store the data inside the hosts filesystem apart from dockers virtual filesystem.
Basically there are 3 ways to persist the data-
* Volume 
* Bind mount
* tmpfs mount (Linux)

![Ways to persist data](https://docs.docker.com/storage/images/types-of-mounts-volume.png)

However Docker recommends the use of Volume as your primary choice for persisting database because of its fair advantages over the other, which includes easy and secured migrating and backup between containers and systems, flexibility on working on linux and windows, user can easily communicate to volumes using Docker Client CLI, etc.

``` 
# to create a volume 
docker volume <volume-name>

# to list all volumes
docker volume ls

# to delete a volume
docker volume rm <volume-name> 
```

> ----

#### What next?

Let's consider you have more than 4-5 containers on your machine and you want to scale them up, configure their networks, test, deploy and manage them. Some organisations even have thousands of containers to manage. Managing containers becomes difficult as they scale up. So we need a tool that take care of our containers.
That's where Container Orchestration comes in picture. Container Orchestration deploys, scales, removes, checks containers health, load balances the traffic and manages all the containers. And the most widely used Container Orchestration tool is Kubernetes. 
So now you know what to explore next!


Connect with me here https://about.me/atharvashinde
:)
