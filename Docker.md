#### What is Docker and why is it used?
Docker is a platform used for building containerised applications. Docker packages a software into a container which contains all its dependencies, libraries, runtimes and other building tools required to run that application on any working environment. Due to its high portability, developers can focus on actual development of the application than worrying about the setup process and its dependencies because of switching workloads. With docker we can manage containers, images, volumes and configure its network. To interact with docker we can either use Docker API or Docker CLI commands. 

### Docker Architecture
![Docker Architecture](https://docs.docker.com/engine/images/architecture.svg)

Docker implements client-server architecture. So what is client-server architecture? The lay-man example for understanding the architecture is Online Shopping. You (client) orders some product from the application and the service-provider (server) places the order, takes necessary actions and ships it to your address. Client requests a service and server side works and provides the desired service.
Referencing the above diagram, if user wants to create a container from one of the installed images and therefore enters the corresponding `docker run` command, docker daemon responds to the request and works accordingly to give desired result.

### What is Docker Daemon?
Daemon is a program that runs consistently in the background when particular action or event is triggered and is not under any direct control of user, that means user cannot change the nature of program. Usually daemon files/processes names are suffixed by 'd', for example:- *sshd, mysqld, dockerd.*
![Docker Workflow](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.oreilly.com%2Flibrary%2Fview%2Fcontinuous-delivery-with%2F9781787125230%2Fassets%2Fcadc3363-6814-489b-a770-58dd9ead6f56.png&f=1&nofb=1)
Docker Daemon listens to API requests/ CLI commands by user and manages docker objects like images, containers, volumes, network.

### Docker Image
Docker Image is built of read-only stacked layers generated from instructions inside the image's dockerfile. Each layer is a representation of an instruction from the dockerfile. Images are pre-built by developers and are available at Container-Registry, a place to store and download images. One such popular public registry is DockerHub. Some companies also have private registries to store their images confidentially.

```
# to install an image in your system
docker pull <image-name:version>
# example docker pull ubuntu:20.04

# to see if the image is installed
docker image ls
# or
docker images

# to remove a image 
docker image rm <image-name or image-id>
# if you get an error message similar to daemon: conflict: unable to delete, then you must delete the container first
read more about containers below 

# to check layers of a image
docker image inspect <image-name or image-id>
```

### Dockerfile
To build your customised docker image create a Dockerfile with extension `.dockerfile` . A new layer is stacked for every new instruction you define inside Dockerfile.

Following is an example of dockerfile
```
# this is how you write a comment
FROM ubuntu:18.04
LABEL org.opencontainers.image.authors="org@example.com"
COPY . /app
RUN make /app
RUN rm -r $HOME/.cache
CMD python /app/app.py
```

### .dockignore
If you have worked with GitHub before you may have used .gitignore file to exclude .env variables, dependency directories, temporary files etc. Similarly for Docker we have `.dockignore` file to exclude files that are not relevant to the build.
Before client request through CLI or API reaches docker daemon it goes through .dockignore file and checks whether there is a context that needs to be excluded before passing to the daemon and thus preventing any large or sensitive information from reaching the daemon.

### Docker Container
Containers are isolated processes which run on a single host machine. Containers consists of packages and dependencies required by your application. We can create, start, stop, delete, move, modify containers which is possible because of a thin writable layer know as 'Container Layer' built on top of immutable read-only image layers. Each container has its own binaries, dependencies, and container-layer therefore each container being an isolated process make them fast, light-weight and more efficient.
Below is an example of layers structure-
![Image structure](https://docs.docker.com/storage/storagedriver/images/container-layers.jpg)
P.S- If user downloads two or more version of same image, docker only builds layer new to version and all the layers which are mutual won't be downloaded again.

 
We can talk to containers either with Docker API or CLI and perform CRUD operations. 

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

So what's the catch? Container when deleted or restarted, loses all its data and starts again from its image definition. So when we delete/restart a container the data inside 'container-layer' is lost and it starts from a fresh state. Now if we try to install/restart it again, the container layer is created from scratch not having any history of operations we did inside previous one. How do we solve this? 

### Persistent data
Persistent data is the solution to the above problem. The idea is to store the data inside the hosts filesystem apart from dockers virtual filesystem.
Basically there are 3 ways to persist the data-
* Volume 
* Bind mount
* tmpfs mount (Linux)

![Ways to persist data](https://docs.docker.com/storage/images/types-of-mounts-volume.png)

However Docker recommends the use of Volume as your primary choice for persisting database because of its fair advantages over the other, which includes easy migrating and backup between containers and systems, secured sharing among multiple containers, flexibility on working on linux and windows, user can communicate to volumes using docker API and CLI, etc.

``` 
# to create a volume 
docker volume <volume-name>

# to list all volumes
docker volume ls

# to delete a volume
docker volume rm <volume-name> 
```

#### Whew! that was just a sneak-peek into docker. So what now?
You now know how to create and manage a container. But there is more than just containers. There are pods, nodes, clusters, networking, monitoring and much more.

Now lets consider that you have more than 4-5 containers and you want to scale them up, configure their networks, deploy and manage them. Some enterprises even have thousands of containers to manage. And managing single container at a time is really not of any help. So there needs to be a tool that manages deploys, scale and take care of our containers.
That's where Container Orchestration comes in picture. Container Orchestration deploys, scales, removes, checks container health, load balances the traffic and manages all the containers.
And the most widely used Container Orchestration tool is Kubernetes. 
