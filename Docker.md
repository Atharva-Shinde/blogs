Ever tried running your code to a different workspace but it broke out in other systems? Docker is here to ease your work, and not just for locally sharing your codebase but much more!


#### What is Docker?
Docker is a platform that allows developers to containerise, build, test, deploy and ship applications seamlessly within multiple workspaces and making it ready for production deployments.

#### Why Docker?
Docker streamlines the development processes by letting us have control over managing workloads. Using docker-based containerised application we can easily ship codebase within different systems/environments without need to worry about setting up libraries and all other configuration files from scratch. With its simple CLI commands we can easily build, delete, deploy and manage containerised images in our local machine. Docker being lightweight and portable makes it a cost-effective alternative to hypervisor virtual machines. Moreover these containers are highly portable which enables them to be able to run on local systems, virtual machines, cloud providers or hybrid workspaces. So if you need fast, lightweight, efficient and orchestrated way to run, scale, deploy or test your application/software on one or more virtualised/physical systems, Docker is your solution.


### Docker Architecture
![Docker Architecture](https://docs.docker.com/engine/images/architecture.svg)

Docker implements client-server architecture. So what is client-server architecture? Consider Online Shopping. You (the client) order some product from app-store and the service-provider (server) places the order, takes necessary actions and ships it to your address. That is client requests a service and the service provider works on the requests and provides the desired state.
Referring the above diagram, if user wants to create a container from one of the installed images and therefore enters its corresponding `docker run` command, docker daemon responds to the request and gives us a configured virtualised container along with its configurations.

### What is Docker Daemon?
Daemon is a program that runs consistently in the background and responds to particular request, and is not under any direct control of user, that means user cannot change the nature of program. Usually daemon files/processes names are suffixed by 'd', for example:- *sshd, mysqld, dockerd.*
![Docker Workflow](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.oreilly.com%2Flibrary%2Fview%2Fcontinuous-delivery-with%2F9781787125230%2Fassets%2Fcadc3363-6814-489b-a770-58dd9ead6f56.png&f=1&nofb=1)
Docker Daemon listens to Docker Client through REST API and manages docker objects like images, containers, volumes, network.

#### What is Docker Client?
Docker client is the primary way to interact with Docker. When we run a Docker command through terminal the client sends the request to Docker Daemon which is responsible for managing commands.

### Docker Image
Docker Image is built of read-only stacked layers generated from instructions inside the image's dockerfile. Each layer is a representation of an instruction from the dockerfile. Images that are pre-built by developers and are available at Container-Registry, a place to store and download images. One such popular public registry is DockerHub. Some companies also have private registries to store their images confidentially.

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
To build your customised docker image create a Dockerfile with extension `.dockerfile`. A new image layer is stacked for an instruction you define inside Dockerfile.

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
Before a request from docker clients CLI reaches docker daemon it goes through `.dockignore` file and checks whether there is a context that needs to be excluded before passing to the daemon and thus preventing any large or sensitive information from reaching the daemon.

### Docker Container
Containers are isolated processes which run on a single host machine. Containers consists of packages and dependencies required by your application to run in your system. We can create, start, stop, delete, move and modify containers which is performed in a thin writable layer know as 'Container Layer' built on top of immutable, read-only image layers. Each container has its own binaries, dependencies, and container-layer therefore each container being an isolated process make them fast, light-weight and more efficient.
Below is an example of layers structure-
![Image structure](https://docs.docker.com/storage/storagedriver/images/container-layers.jpg)
P.S- If user downloads two or more version of same image, docker only builds the layers which are new from previous versions and all the layers which are mutual won't be downloaded again.

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

So what's the catch? Containers are not persistent. Container when deleted or restarted, loses all its data and starts again from its image definition. So when we delete/restart a container the data inside 'container-layer' is lost and it starts from a fresh state. Now if we try to install/restart it again, the container layer is created from scratch not having any history of operations we did inside previous one. How do we solve this? 

### Persistent data
Persisting database is the solution to the above conflict. The idea is to store the data inside the hosts filesystem apart from dockers virtual filesystem.
Basically there are 3 ways to persist the data-
* Volume 
* Bind mount
* tmpfs mount (Linux)

![Ways to persist data](https://docs.docker.com/storage/images/types-of-mounts-volume.png)

However Docker recommends the use of Volume as your primary choice for persisting database because of its fair advantages over the other, which includes easy migrating and backup between containers and systems, secured sharing among multiple containers, flexibility on working on linux and windows, user can communicate to volumes using Docker Client CLI, etc.

``` 
# to create a volume 
docker volume <volume-name>

# to list all volumes
docker volume ls

# to delete a volume
docker volume rm <volume-name> 
```

#### Whew! that was just a sneak-peek into docker. So what now?
You now know basic ideology behind Docker and its containers and images. But there is more than just containers and images. There are pods, nodes, clusters, networking, monitoring and much more.

Lets consider that you have more than 4-5 containers and you want to scale them up, configure their networks, test, deploy and manage them. Some enterprises even have thousands of containers to manage. Managing these many containers is pain. So there needs to be a tool that manages deploys, scale and basically take care of our containers.
That's where Container Orchestration comes in picture. Container Orchestration deploys, scales, removes, checks container health, load balances the traffic and manages all the containers.
And the most widely used Container Orchestration tool is Kubernetes. 

So now you know where to go next.
 
