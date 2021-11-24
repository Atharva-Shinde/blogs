#### What is Docker and why is it used?
Docker is platform for building containerised applications and running it on any Linux server. Docker enables user to work on multiple environments. Due to its high portability, developers can focus on actual development of the application than worrying about the setup process and its dependencies because of switching workloads. This 

#### Docker Architecture
![Docker Architecture](https://docs.docker.com/engine/images/architecture.svg)

Docker implements client-server architecture. So what is client-server architecture? The lay-man example for understanding the architecture is Online Shopping. You (client) orders some product from the application and the service-provider (server) places the order, takes necessary actions and ships it to your address. Client requests a service and server side works and provides the desired service.
Referencing the above diagram, if user wants to create a container from one of the installed images and therefore enters the corresponding `docker run` command, docker daemon responds to the request and works accordingly to give desired result.

#### What is Docker Daemon
Daemon is a program that runs consistently in the background when particular action or event is triggered and is not under any direct control of user, that means user cannot change the nature of program. Usually daemon files/processes names are suffixed by 'd', for example:- *sshd, mysqld, dockerd.*
![Docker Workflow](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.oreilly.com%2Flibrary%2Fview%2Fcontinuous-delivery-with%2F9781787125230%2Fassets%2Fcadc3363-6814-489b-a770-58dd9ead6f56.png&f=1&nofb=1)
Docker Daemon listens to API requests/ CLI commands by user and manages docker objects like images, containers, volumes, network.

#### Dockerfile
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

#### Docker Image
Docker Image is built of read-only stacked layers generated from instructions inside the image's dockerfile. Each layer is a representation of an instruction from the dockerfile. Images are pre-built by developers and are available at Container-Registry, a place to store and download images. One such popular public registry is DockerHub. Some companies also have private registries to store their images confidentially.

#### Docker Container
Containers are isolated processes which run on a single host machine. Containers consists of packages and dependencies required by your application. We can create, start, stop, delete, move, modify containers which is possible because of a thin writable layer know as 'Container Layer' built on top of immutable read-only image layers. Each container has its own binaries, dependencies, and container-layer therefore each container being an isolated process make them fast, light-weight and more efficient.
Below is an example of layers structure-
![Image structure](https://docs.docker.com/storage/storagedriver/images/container-layers.jpg)
P.S- If user downloads two or more version of same image, docker only builds layer new to version and all the layers which are common won't be downloaded again.
 
We can talk to containers either with Docker API or CLI and perform CRUD operations. 

Containers helps in setting up environment on any OS without worrying about configurations and dependencies, and actually focusing on building applications. Containers being lightweight and portable reduces time required to build environment from scratch.

So what's the catch? Container when deleted or restarted, loses all its data and starts again from its image definition. So when we delete/restart a container the data inside 'container-layer' is lost and it starts from a fresh state. Now if we try to install/restart it again, the container layer is created from scratch not having any history of operations we did inside previous one. How do we solve this? 

