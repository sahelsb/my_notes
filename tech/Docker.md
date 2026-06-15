# Docker

## what is Devops ?

**Devops** is the collaboration between the developer and operation teams, which enables continuous delivery of applications and services to the end users.

DevOps is a development methodology aimed at bridging the gap between Development and Operations, emphasizing communication and collaboration, continuous integration, quality assurance and delivery with automated deployment utilizing a set of development practices

![](Devops.png)

Developers team  vs   Operation team

## What is **Docker**?

Containerization involves encapsulating or packaging up software code and all its dependencies so that it can run uniformly and consistently on any infrastructure.
- Develop and run the application inside an isolated environment (known as a container) that matches your final deployment environment.
- Put your application inside a single file (known as an image) along with all its dependencies and necessary deployment configurations.
- And share that image through a central server (known as a registry) that is accessible by anyone with proper authorization.

**Docker** is a containerization platform which is used to automate the deployment of applications in a lightweight container so that applications can work efficiently in different environments. These containers are isolated so that they don't interfere with each other

Note: container is a software package that consists of application and all the dependencies required to run an application

1. Docker is a set of tools to deliver software in containers.
2. Containers are packages of software.

Just imagine that we want to develop software applications that each has its own specific framework, docker provides the suitable framework for each application.

Now that docker provides each application with its framework, we can use the area we use before for storing the frameworks , now for another application. 

#### Docker Benefits :

##### Scenario 1: Works on my machine

First you plan an application. Then your team of 1-n developers create the software. It works on your computer. You send it to the server and......it does not work.
This is known as the **"works on my machine"** problem. The only way to solve this is by finding out what in tarnation the developer had installed on their machine that made the application work.

Containers solve this problem by allowing the developer to personally run the application inside a container, which then includes all of the dependencies required for the app to work.

##### Scenario 2: Isolated environments

You have 5 different Python applications. You need to deploy them to a server that already has an application requiring Python 2.7 and of course none of your applications are 2.7. What do you do?

Since containers package the software with all of its dependencies, you package the existing app and all 5 new ones with their respective Python versions and that's it.

##### Scenario 3: Development

You are brought into a dev team. They run a web app that uses other services when running: a Postgres database, MongoDB, Redis and a number of others. Simple enough, you install whatever is required to run the application and all of the applications that it depends on...

What a headache to start installing and then managing the development databases on your own machine.With one command you get an isolated application, like Postgres or Mongo, running in your machine.


#### Without docker :

![](NoDocker.png)

#### Without docker the same oracle WebLogic should installed multiple times :

![](NoDocker2.png)


#### With docker : 

![](WithDocker.png)


## How does Docker work 

![](DockerEngine.png)

### Docker components :

![](DockerComponents.png)

### Docker client and server :

- Docker client is accessed from a terminal and a docker server runs the docker daemon and registry
- A user can build docker images and run docker containers by passing commands tp docker client. The client then use the REST API to reach out to the long running daemon and the dameon get your work done.


1. **Docker Daemon:** The daemon (`dockerd`) is a process that keeps running in the background and waits for commands from the client. The daemon is capable of managing various Docker objects.
2. **Docker Client:** The client (`docker`) is a command-line interface program mostly responsible for transporting commands issued by users.
3. **REST API:** The REST API acts as a bridge between the daemon and the client. Any command issued using the client passes through the API to finally reach the daemon.


![](DockerServer.png)

### Docker images :

- Docker image is a template with instructions which is used for creating docker containers
- Docker image is built using a file called Docker file
- Docker image is stored in a docker file or repository (like registry.hub.Docker.com)

This allows other people to access the same structure of a docker environment that you have created

Syntax for creating a docker container using docker image :

### Docker container :

![](DockerContainer.png)


### Docker Registry :

Now with a lot of people working on your project you want to let all the people access the docker image so docker registry is for this. An image registry is a centralized place where you can upload your images and can also download images created by others. [Docker Hub](https://hub.docker.com/) is the default public registry for Docker.


![](DockerRegistry2.png)


### Recap :

![](Recap.png)


### Installing docker : 

To install the docker and docker compose you only need to install docker desktop and it installs all the necessary docker tools you need on your computer

Note : you should run docker desktop as administrator after installation

Note : you need to install update WSL2 linux kernel on your computer

This command gives you the version of docker installed on ur pc

```
        docker version && docker-compose version
```


### Containers vs Images

Instead of virtualizing the entire physical machine, containers virtualize the host operating system only. Just like virtual machines, containers are completely isolated environments from the host system as well as from each other. 

Think of a container as a ready-to-eat meal that you can simply heat up and consume. An image, on the other hand, is the recipe or ingredients for that meal. 
 you need an image and a container runtime (Docker engine) to create a container. The image provides all the necessary instructions and dependencies for the container to run, just like a recipe provides the steps and ingredients to make a meal.
 In short, an image is like a blueprint or template, while a container is an instance of that blueprint or template.

##### Containers vs Virtual Machines

Virtual machines are usually created and managed by a program known as a hypervisor, like VMware workstation , VirtualBox and so on. This hypervisor program usually sits between the host operating system and the virtual machines to act as a medium of communication.

Each virtual machine comes with its own guest operating system which is just as heavy as the host operating system. The application running inside a virtual machine communicates with the guest operating system, which talks to the hypervisor, which then in turn talks to the host operating system to allocate necessary resources from the physical infrastructure to the running application.

Unlike a virtual machine, a container does the job of virtualization in a smarter way. Instead of having a complete guest operating system inside a container, it just utilizes the host operating system via the container runtime while maintaining isolation. The container runtime, that is Docker, sits between the containers and the host operating system instead of a hypervisor. The containers then communicate with the container runtime which then communicates with the host operating system to get necessary resources from the physical infrastructure.
containers use the WSL2 kernel. It happens because WSL2 acts as the back-end for Docker on Windows.
‌

#### Image

A Docker image is a file. An image never changes; you can not edit an existing file. Creating a new image happens by starting from a base image and adding new **layers** to it. 
List all your images with `docker image ls`
This image file is built from an instructional file named **Dockerfile** that is parsed when you run

```
docker image build -t <image name>:<tag name> .    # create the image

docker container run -it <image name>:<image tag>    # run a new container
```

To perform an image build, the daemon needs two very specific pieces of information. These are the name of the `Dockerfile` and the build context. In the command issued above:

- `docker image build` is the command for building the image. The daemon finds any file named `Dockerfile` within the **context**.
- The `.` at the end sets the context for this build. The context means the **directory accessible by the daemon** during the build process.

##### Tagging an image
you can assign custom identifiers to your images instead of relying on the randomly generated ID.
the default tag for each image is `latest` which is the latest version of an image.

```
--tag <image repository>:<image tag>
```
The repository is usually known as the image name and the tag indicates a certain build or version.

##### Remove an Image
To remove the image , `docker image rm <image ID>.
The identifier can be the image ID or image repository.

If you use the repository, you'll have to identify the tag as well. `docker image rm alpine:latest`

###### Dockerfile
is the instruction set for building an image, once processed by the daemon, results in an image. So Dockerfile is the recipe for an image and an image is the recipe for a container. The only difference is that Dockerfile is written by us, whereas image is written by our machine based on the Dockerfile!
Images are multi-layered files and in this file, each line (known as instructions) that you've written creates a layer for your image.

```
# This a comment , but a comment should be only in the begining of a line

# set the base image for the resultat image
FROM <image>:<tag>     

# port that needs to be published
Expose 80            

# executes a command inside the container
RUN <install some dependencies>    

# default command  
CMD <command that is executed on `docker container run`>    
```

#### Containers

Containers only contain what is required to execute an application; and you can start, stop and interact with them. They are **isolated** environments in the host machine with the ability to interact with each other and the host machine itself via defined methods (TCP/UDP).

##### List containers
List all your containers with `docker ps` OR `docker container ls`
Without `-a` flag it will only print running containers

containers have a _CONTAINER ID_ and _NAME_. The names are currently autogenerated. When we have a lot of different containers, we can use grep to filter the list: `docker container ls -a | grep hello-world`

##### Rename a container
Naming a container can be achieved using the `--name` option.

```bash
docker container run --name first-container  hello-world
```

##### Run a container
You can run a container from an image by `docker [container] run <image name>`, which instructs daemon to **create a new container** from the image and downloading the image if it is not available. once an image has been fetched, it'll stay in the local cache

This means that we can pull and run any public image from Docker's servers. For example‚ if we wanted to start an instance of the PostgreSQL database, we could just run `docker run postgres`, which would pull and run. We can search for images in the Docker Hub with `docker search`

###### Download an image
you can also download/pull images from docker registry without running them: 

```
docker image pull <image name>[:<tag name>]
```


When you run a command, e.g. `docker container run`, behind the scenes the client sends a request through the REST API to the **Docker daemon** which takes care of images, containers and other resources.

##### Interactive Container
Popular distributions such as **Ubuntu** all have official Docker images available in the hub. Programming languages such as **python** all have their official images. These images do not just run some pre-configured program. These are instead configured to run a shell by default. 

shells are interactive programs. An image configured to run such a program is an interactive image.
These images require a special `-it` option to be passed in the `container run` command. This allows you to interact with the container by using the command line.


```
docker container run  -it ubuntu
OR 
docker container run  --interactive --tty sh
```
by this command you run a container in interactive mode, you should land directly on bash or shell inside the Ubuntu container.

- `-i` attaches standard in (stdin) to the process running inside the container that allows us to send commands to the shell running inside the container.

##### Publish a service to a port
Containers are isolated environments. Your host system doesn't know anything about what's going on inside a container. Hence, applications running inside a container remain inaccessible from the outside.
To allow access from outside of a container (e.g. access the web service which is running in the container), you must publish the appropriate port inside the container to a port on your local network. The common syntax for the `--publish` or `-p` option is as follows:

```
docker run hello-world   --publish[OR -p] <host port>:<container port>
docker run hello-world   --publish 8080:80
```
it means any request sent to port 8080 of your host system will be forwarded to port 80 inside the container‌. Now to access the application on your browser, visit `http://127.0.0.1:8080`.
Please pay attention that for each conatiner you have to specify a different port.

##### Detached Mode
in order for the container to keep running, you had to keep the terminal window open. Closing the terminal window also stopped the running container.

This is because, by default, containers run in the foreground and attach themselves to the terminal like any other normal program invoked from the terminal.

In order to override this behavior and keep a container running in background, you can include the `--detach` option with the `run` command as follows:

```
docker container run --detach[OR -d] --publish 8080:80 hello-world
```

##### Attach to a Container
Use `docker attach` to attach your terminal's standard input, output, and error (or any combination of the three) to a running container using the container's ID or name. This lets you view its output or control it interactively, as though the commands were running directly in your terminal.

```
docker container attach <ContainerID>
```

##### Execute a command inside the container
you can start a second program (executes a command) inside the container that is running e.g. for debugging purposes, by `docker container exec `command`

```
docker container exec c1 cat /etc/nginx/nginx.conf
docker container exec -it c1 sh              # executes a shell inside container
```
##### Check the kernel that container uses
```
uname -r          # shared the opearting system kernel
```

##### Execute a command inside a container
passing a command to a container that is not running

```
docker container run <image name> <command>
```

##### Container Volumes
Images are made of a set of read-only layers. When we start a new container, Docker adds a read-write layer on top of the image layers enabling the container to run.
Any file change inside the container creates a working copy in the read-write layer of the docker image. However any data or changes created inside a container is lost once that container is removed or stopped. 
Any run of the container again starts with a clean filesystem. If we want to keep data between runs Volumes are the solution. They’re designed to persist data outside of the container’s lifecycle, enabling us to store and manage data that must survive when a container is removed or the image is rebuilt. Docker volumes, store and manage the essential elements for your application.

##### 1. Bind Mounts
A Docker bind mount is a high-performance connection from the container to a directory on the host machine. **It enables the host to share its filesystem with the container**, which can be made read-only or read-write.
You can use the option` --volume [OR -v]` to make a local directory available in the container.
This is a simple way to provide persistent files between invocations of a Docker container. Still, it’s often most useful for when the container is doing work on behalf of the host.

```
docker container run -p 80:80 -v /local directory path:/usr/share/nginx/html nginx
docker container run -p 80:80 -v /Users/html:/usr/share/nginx/html nginx
```

##### 2. Docker Volumes
A bind mount uses the host filesystem, but **Docker volumes are native to Docker**. The data is kept somewhere on storage attached to the host, most often the local filesystem. The volume itself has a lifecycle that’s longer than the container’s, enabling it to persist until no longer needed. Volumes can be shared between containers.

```
docker volume create data_volume    # create a volume
docker volume ls                    # list all volumes
docker volume rm data_volume        # remove volume
```

##### Stop a container
Containers running in the foreground can be stopped by simply closing the terminal window or hitting `ctrl + c`. Containers running in the background, however, can not be stopped in the same way. To stop these containers using 

```
docker container stop <container ID or name>
```

The `docker stop` command shuts down a container gracefully by sending a `SIGTERM` signal. If the container doesn't stop within a certain period, a `SIGKILL` signal is sent which shuts down the container immediately, whereas the `docker kill` commands sends the **SIGKILL** signal. The execution of the SIGTERM and SIGKILL is different. Unlike SIGKILL, the SIGTERM gracefully terminates a process rather than killing it immediately. SIGTERM allows a child process or parent process the opportunity to send information to other processes.

```
docker container kill <container ID>
```

###### PID 1
pressing `ctrl + c` when you are attached to a container just forwards the SIGINT signal to the PID 1 of the container and the container exists as soon as the PID 1 terminates. This means that as long as the PID 1 is alive the container will stay alive.

##### Restart a container
stopped containers remain in your system. If you want you can restart them. The `container start` command can be used to start any stopped or killed container. The syntax of the command is as follows:

```
docker container start <container ID>
```

Now, in scenarios where you would like to reboot a running container you may use the `container restart` command.

```
docker container restart <container ID>
```

##### Remove containers / Images
To remove the image , `docker image rm <image ID>.
The identifier can be the image ID or image repository. If you use the repository, you'll have to identify the tag as well.

before removing images, you should have the referencing container removed first.
remove the container with `docker container rm <container ID>` , It accepts a container's name or ID as its arguments.
Or, instead of removing individual containers, if you want to remove all dangling containers at one go, you can use the `container prune` command.

There is also the `--rm` option for the `container run` and `container start` commands which indicates that you want the containers removed as soon as they're stopped.

```
docker container run --rm hello-world
```


##### Stop all containers

```docker stop $(docker ps -aq)```

##### Remove all containers at once

```docker container rm $(docker container ls -aq)```

##### Create a Container without Running
`container create <image>` command creates a container from a given image.
`container start <Container ID>` command starts a container that has been already created.


#### Check running process
```
ps -ef
```
if you run this command inside a container you will only see the process running in that specific container, so docker containers are running in isolation.

##### Checking IP address
containers has different IP addresses   `ip addr`

You can ping IP address of one container from another `ping <IP address>`

#### Communication of containers

You can use the option `--link` to link one container to other and then you can refer to the other container with its name like this : `ping c1`

```
docker container run --rm -it --name c2 --link c1 alpine sh
```

But `--link` is deprecated so we use :

##### User defined Networks
 
 we use the option `--network` :
 ```
docker network ls
docker network create test       # create a new network
docker container run -it --rm --network test --name c1 alpine sh
```
 
 In a second terminal :
```
docker container run -it --rm --network test --name c2 alpine sh
ping c1
```

to remove the network : 
```
docker network rm test
```

#### Use `--help`  flag 
you can use this flag to get more info about a command  `docker container --help`


### PostgreSQL

If you want to use docker with a database you need a client to operate on and the client that we use is **adminer** (formerly phpMyadmin)


```
docker-compose up db adminer
```

you can start PostgreSQL as docker container ( $ docker-compose up), It will also start Adminer ($ db adminer) which is a simple database management UI. It allows you to query the database and alter tables within the database. You can access the ui via [http://localhost:8090/]

### What is adminer?

Adminer (formerly phpMinAdmin) is  **a full-featured web-based database management tool written in PHP**. Conversely to phpMyAdmin, it consist of a single file ready to deploy to the target server. Adminer is available for MySQL, PostgreSQL, SQLite, MS SQL, Oracle, Firebird, SimpleDB, Elasticsearch and MongoDB

### What is compose.yml file ?

A **docker-compose.yml** is a **config file** for [Docker Compose]

It allows to deploy, combine, and configure multiple docker containers at the same time. The Docker "rule" is to outsource every single process to its own Docker container.

Take for example a simple web application: You need a server, a database, and PHP. So you can set three docker containers with Apache2, PHP, and MySQL.

The advantage of Docker Compose is easy configuration. You don't have to write a big bunch of commands into Bash. You can predefine it in the **docker-compose.yml** like below :

```
# compose file format version
version : `3.3`     

# specifying containers in the service tag
services:
	# service name for configuring different containers
	web:
		image: nginx:latest
		ports:
			- 80:80
		volumes:
			-./html:/usr/share/nginx/html         # host:container
		build:
			context: .         # give the path to the dockerfile

	pg:
		image: postgres:9.6-alpline
		environment:
		 - POSTGRES_DB=test
		env_file:
		 - ./db/env
```

#### Docker Compose 

Docker Compose is designed to simplify running multi-container applications using a single command.

In short, Docker Compose works by applying many rules declared within  a single docker-compose.yml configuration file

These [YAML] rules, both human-readable and machine-optimized, provide us an effective way to snapshot the whole project from ten-thousand feet in a few lines.

#### in the end we just need to run :
```
# it will run all the services with its containers
docker-compose up
docker-compose up -d
```

```
# This will run only the containers for the service pg
docker-compose up <service_name>
```

##### In order to list all containers we use :
```
docker-compose ps
```

##### Stop and delete all containers :
```
docker-compose stop <service_name>
docker-compose rm  <service_name>
```

##### Build images :

```
docker-compose build
docker-compose build  <service_name>

# This will build images and create containers based on those images
docker-compose up --build
```
#### What is the difference between dockerfile and docker-compose

The contents of a Dockerfile describe how to _create_ and _build_ a Docker image, while docker-compose is a command that runs Docker containers based on settings described in a _docker-compose.yaml_ file.

#### Remote debugging

You're likely familiar with local debugging—the ability to go through your code line by line to find and eliminate bugs. However, with the ever-increasing complexity of development environments, working efficiently with remote systems is becoming more necessary. In this case, "remote" can mean any machine you don't have native OS-level access to, such as Virtual Machines, Docker containers, and entirely separate devices accessed over the network.

With remote debugging, you can work with these systems more effectively by connecting your development tools to an application running outside your local environment

**A common use case for remote development is when working with ** [Docker containers] It can be beneficial to connect to the code running inside the container to debug your applications directly

Another increasingly popular option that can be considered remote development is for developers using Windows machines who want to use WSL as their primary development environment.