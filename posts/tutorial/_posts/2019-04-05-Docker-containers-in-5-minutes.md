---
github: docker-tutorial
---

<kbd class="imgtitle">Contents</kbd>

- [Overview](#overview)
- [Creating Dockerfile](#creating-dockerfile)
- [Building Docker image](#building-docker-image)
- [Run as Container](#run-as-container)
- [Common facilities](#common-facilities)
- [Other facilities](#other-facilities)
- [Reference](#references)
{: .contentBorder .txt-pad}

### Overview

This post explains about the steps involved in containerizing an application using <mark>docker</mark> tool.
Also tried to disclose an overview on other areas related to this topic.

> Containers are an abstraction at application layer that packages the codes and dependencies together, 
ships the application and run-time environment.

Container are running on the <mark>docker engine</mark> almost as VM but not exactly. It has lot of merits in production basis
and currently it is booming in IT-Industry now. For example containerizing an application with *docker* or *kubernetes* provides
enormous facilities.

<br>
In simple, we can say that, we are going to releasing our application as an image which will run as a bounded isolated OS 
instead of releasing it without the environments and dependencies. It will fully reduce the environment and dependency problems which we often facing.

Totally we are just going to follow these three steps in overall. The steps are,

|       | File system |Details|
|-------|-------------|-------|
|Build | Dockerfile   | Packaging the application with required dependencies and custom files| 
|Ship  | Docker image | Releasing it as an image file globally using <mark>docker registry</mark>|
|Run   | Container    | Run containers using the image which will act as your application along with an isolated VM like environment|
{: .dataframe style="margin:5%;"}

For very basic level, To understand the containers, I am just going to containerize a simple file printer shown below,

```python
filename = "log.txt"
myfile = open(filename, 'w')
myfile.write( "Hi Here we are ..!" + '\n')
myfile.close()
``` 

This code just create and save the content in a file named <mark>log.txt</mark>. Lets containerise.. see what is happening ... !

### Creating Dockerfile

Dockerfile is also like a <mark>Makefile</mark>, which is used to build the docker image. This file normally contains three type of instruction
sets,

- Fundamental instruction
- Configuration instruction
- Execution instruction

For our scenario, The dockerfile would be like this,

```text
FROM python:2
COPY test.py /usr/
WORKDIR /usr/
RUN python test.py
CMD bash
```

Description :
- <mark>FROM</mark> command determines the base image. you can use <mark>scratch</mark> if you have total cross compiled system.
- <mark>COPY</mark> command just copying your local file into your container location.
- <mark>WORKDIR</mark> command changes the current directory for next command executions.
- <mark>RUN</mark> command executes the command inside the container.
- <mark>CMD</mark> is the container launching command. container will live until it runs.

### Building Docker image

Go to the build directory and make sure you have <mark>Dockerfile</mark> in your current directory.
To build the docker image use the command,

```commandline
docker build -t testimage .
``` 

Sending build context to Docker daemon  3.072kB
Step 1/5 : FROM python:2
 ---> 92c086fc9702
Step 2/5 : COPY test.py /usr/
 ---> Using cache
 ---> 1b9aa6ce04cd
Step 3/5 : WORKDIR /usr/
 ---> Using cache
 ---> 6dcef3ef8785
Step 4/5 : RUN python test.py
 ---> Using cache
 ---> 6edf4708cf6c
Step 5/5 : CMD bash
 ---> Using cache
 ---> 21303e2891d6
Successfully built 21303e2891d6
Successfully tagged testimage:latest
{: .output}

This command creates an image with the name and version you provided. When you build,

- If the base image not available in your local, It will pull it from <mark>Docker Hub<mark> registry.
- It creates layers for each commands inside the docker file and It will be remembered by docker.
- If any thing changed after once build, It will create new layers for that.
- You can't use **Capitals** in image name.

You can check the created image by listing available images using the command,

```commandline
docker image ls
```
or you can also specify the command

```commandline
docker image ls testimage
```

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
testimage           latest              21303e2891d6        3 days ago          914MB
{: .output}

### Run as Container

**Method 1 :**

We can containerize this image using, two steps.
```commandline
docker container create --name testcontainer testimage
docker container start testcontainer
```

**Method 2 :**

Or it can be done in single step by,

```commandline
docker run -itd --name testcontainer testimage
```

The arguments <mark>itd</mark> means interactive, tty and detach. See the help for more details.
we can check the container status using the command

```commandline
docker container ls
```

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
c706bd3fe268        testimage           "/bin/sh -c bash"   5 seconds ago       Up 3 seconds                            testcontainer
{: .output}

we can enter inside the container using <mark>exec</mark> facility with **bash** command like shown below,

```commandline
docker exec -it testcontainer bash 
```

Inside the container environment,

root@c706bd3fe268:/usr# ls
bin  games  include  lib  local  log.txt  sbin  share  src	test.py
{: .output}

Here we can see the file <mark>log.txt</mark> which was generated while this container started.

### Common facilities

I always suggest to see this official [documentation](https://docs.docker.com/engine/reference/commandline/docker/) for commands.
But here i have shared often some using commands and also felt useful for quick view :).

Some Basic commands,

- <mark>Docker inspect</mark> - Inspecting the information about the custom object.
- <mark>Docker rm</mark> - Removing the object provided in arg.
- <mark>Docker info</mark> - Printing the docker information.
- <mark>Docker rename</mark> - All objects can be renamed.
- <mark>Docker login</mark> - Registry Login
- <mark>Docker logout</mark> - Registry Logout

For Images,
- <mark>Docker image</mark>
- <mark>Docker search</mark> - Search images in customized docker registry.
- <mark>Docker pull</mark> - Pulling images from registry.
- <mark>Docker push</mark> - Pushing images to the customized registry.
- <mark>Docker save</mark> - Save the image as compressed file.
- <mark>Docker load</mark> - Load the compressed file as an image.
- <mark>Docker rmi</mark> - Removing images.
- <mark>Docker run</mark> - Create + Start the container in single command.

For containers,
- <mark>Docker container</mark>
- <mark>Docker ps</mark> - Process status for current running processes.
- <mark>Docker start</mark> - Initiating the container.
- <mark>Docker restart</mark> - Restarting the already started container.
- <mark>Docker cp</mark> - Copy the files from the local directory to the container path.
- <mark>Docker port</mark> - Port mapping on running container.
- <mark>Docker pause</mark> 
- <mark>Docker unpause</mark>

Some Important facilities such as,

- <mark>Docker volume</mark> - Mounting the local directory as a volume object to the container.
- <mark>Docker network</mark> - Network configuration customizing for <mark>bridge</mark>, <mark>vlan</mark> and <mark>overlay</mark> networks.
- <mark>Docker stats</mark> - Statistics on the container information on the machine environment.
- <mark>Docker top</mark> - Normal Top command for quick view.  
- <mark>Docker secret</mark> 
- <mark>Docker plugin</mark>


### Other facilities

Docker has many more awesome facilities such as,

- <mark>Docker compose</mark>

    Composing or managing multiple containers by a single configuration file <mark>docker-compose.yaml</mark>.
    
- <mark>Docker swarm</mark>

    Swarm mode is for managing the docker clusters using manager and worker scenario.
    
- <mark>Docker Service</mark>

    It is used in swarm mode for deploying the application as a service with some facilities such as <mark>rollback</mark>, 
    <mark>scale</mark> and <mark>update</mark>.
    
- <mark>Docker Stack</mark>

    Docker stack is also in swarm mode for managing collection of multiple services.  

These facilities used for <mark>High availability</mark>, <mark>distributed processing</mark>, <mark>scaling</mark>
and <mark>zero down time deployment</mark> (almost).

### References

- [Docker official documentation](https://docs.docker.com/)
- [Docker tutorial](https://github.com/bhanuchander210/docker-tutorial)
- [Docker Cheat Sheet by wsargent](https://github.com/wsargent/docker-cheat-sheet)
- [Docker-Containers-Most-Asked-Questions-and-Answers](https://bhanuchander210.github.io/Docker-Containers-Most-Asked-Questions-and-Answers/)
- [kubernetes](https://kubernetes.io/)