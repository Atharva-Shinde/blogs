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
