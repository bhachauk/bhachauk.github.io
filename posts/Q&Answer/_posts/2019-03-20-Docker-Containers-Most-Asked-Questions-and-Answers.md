---
layout: qanda
---

<br><br>

This post tried to cover the area of rarely shared and highly demanded methods in containerisation with docker and
kubernetes. you can enhance this post by contributing in Docker-tutorial [GitHub](https://github.com/bhachauk/docker-tutorial) repo.
I have added these kind of stuffs under **`## Quick Details`** in every <mark>readme.md</mark> of all chapters.

###### What are the Dockerfile Instructions ?
{: .qandaq}

**Fundamental Instructions**

- <mark>FROM</mark>
    Sets the Base Image for subsequent instructions.
- <mark>ARG</mark>
    Defines a build-time variable.
- <mark>MAINTAINER</mark>
    Deprecated - use LABEL instead) Set the Author field of the generated images.
- <mark>ENV</mark>
    Sets environment variable.
- <mark>LABEL</mark>
    Apply key/value metadata to your images, containers, or daemons.

**Configuration Instructions**

- <mark>RUN</mark>
    Execute any commands in a new layer on top of the current image and commit the results.
- <mark>ADD</mark>
    Copies new files, directories or remote file to container. Invalidates caches. Avoid ADD and use COPY instead.
- <mark>COPY</mark>
    Copies new files or directories to container. Note that this only copies as root, so you have to `chown` manually regardless of your USER / WORKDIR setting, as same as ADD.
- <mark>VOLUME</mark>
    Creates a mount point for externally mounted volumes or other containers.
- <mark>USER</mark>
    Sets the user name for following RUN / CMD / ENTRYPOINT commands.
- <mark>WORKDIR</mark>
    Sets the working directory.

**Execution Instructions**

- <mark>CMD</mark>
    Provide defaults for an executing container.
- <mark>EXPOSE</mark>
    Informs Docker that the container listens on the specified network ports at runtime. NOTE: does not actually make ports accessible.
- <mark>ONBUILD</mark>
    Adds a trigger instruction when the image is used as the base for another build.
- <mark>STOPSIGNAL</mark>
    Sets the system call signal that will be sent to the container to exit.
- <mark>ENTRYPOINT</mark>
    Configures a container that will run as an executable.

######  How to update port Mapping on running Container ?
{: .qandaq}

- Stop and commit a the container as an image.
- Start the snapshot image of our container with port mapping
 
docker stop containerName
docker commit tempImageName
docker run -p 8080:8080 --name -td tempImageName
{: .output}

**Reference :**
  -[An answer in Stackoverflow by Fujimoto Youichi](https://stackoverflow.com/questions/19335444/how-do-i-assign-a-port-mapping-to-an-existing-docker-container)
{: .refbox}


###### How to connect and disconnect containers in docker bridge network ?
{: .qandaq}

Follow these simple steps to connect and disconnect multiple containers with a <mark>bridge</mark> network.

- To create a bridge network with default info

```commandline
docker network create --driver bridge testbridge
```

- Lets start connect containers to these network

```commandline
docker network connect testbridge containerOne
docker network connect testbridge containerTwo
```

- Check the network for containers

```commandline
docker network inspect testbridge
```

"Containers": {
            "2475796b7bb161fafd661eb9e1f23233104ca57915dd88a3fc33aa6dc9d73700": {
                "Name": "containerOne",
                "EndpointID": "45319bd6ce083bf7e7d3015750e35f7644d4a2d3e5db8c27153c613958ab43d2",
                "MacAddress": "02:42:ac:1e:00:03",
                "IPv4Address": "172.30.0.3/16",
                "IPv6Address": ""
            },
            "ae7ca4ac1e4aaa2bab4d53e24f76afa1f83de620d1ce7d244e03cb8707a8448b": {
                "Name": "containerTwo",
                "EndpointID": "166b2c5eea217c9baeeb906c5d83b04d1c1bab93e46ab01bbf6e94fc21c47c81",
                "MacAddress": "02:42:ac:1e:00:02",
                "IPv4Address": "172.30.0.2/16",
                "IPv6Address": ""
            }
        },
....
{: .output}

You can check network by verifying containers from the generated <mark>json</mark> file.

###### How to share the images locally ?
{: .qandaq}

Follow this two reliable steps to share the image as <mark>.tar</mark> compressed file format.
 
- Save that image to as a .tar file.
- Load the image from .tar file

docker save --output imageName.tar imageName
docker load --input imageName.tar
{: .output}

###### What is dangling image ?
{: .qandaq}

Dangling images are created while creating new build of a image without renaming / updating the version. So that
the old image converted into dangling images like shown below.

- List all dangling images

```
$ docker images -f dangling=true
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
<none>              <none>              3f4ae2ddf543        4 days ago          1.37GB
<none>              <none>              b4c8cecab3bc        8 days ago          655MB
```

- To remove all dangling images, Run this command,

$ docker rmi $(docker images -f dangling=true -q)
{: .output}

**Reference :**
    - [What is Dangling images by SO](https://stackoverflow.com/questions/45142528/docker-what-is-a-dangling-image-and-what-is-an-unused-image)
{: .refbox}


### How to import images inside kubernetes cluster in simple way ?
{: .qandaq}

It can be done by configuring the <mark>registry</mark> but i found it helpful. Initially go to the
directory of the build path and make sure you have the <mark>Dockerfile</mark> in your directory.

```
-currentdirectory
       |---  Dockerfile 
       |---  Other-Project-Files
```

- Start minikube

minikube start
{: .output}

- set docker environment by eval in current directory

eval $(minikube docker-env)
{: .output}

- Start build your image now...

docker build -t imageName:version .
{: .output}

- Access the image by changing the image pull policy

kubectl run hello-foo --image=foo:0.0.1 --image-pull-policy=Never
// Or it can be set inside the yaml config file like shown below
 -image: imageName:latest
  name: imageName
  imagePullPolicy: Never
{: .output}


References
  -[Kubernetes official doc](https://kubernetes.io/docs/home/)
  -[How to use local docker images with Minikube? - stackoverflow](https://stackoverflow.com/questions/42564058/how-to-use-local-docker-images-with-minikube)
{: .refbox}

### How Deployment used over Pod and ReplicaSet in kubernetes and Why ?
{: .qandaq}

<img src="https://github.com/bhachauk/docker-tutorial/raw/master/assets/img/replicaset.png" width="500">

The need of ReplicaSet is,

- Pod, basically contains one or more than one containers.
- Pod is the most basic entity in <mark>kubernetes</mark>.
- ReplicaSet is like a manger of Pod which ensures the Pods activity. It always sees Pod as Replica (also like a Job). So that
 it is called as *ReplicaSet* (Set of replicas or Set of Pods).
 
 Running Pod alone is dangerous because,
 
 - When the machine crashes or some thing happens related to it, Pod will be deleted.
 - That's why ReplicaSets are used to provide guarantee for Pod's life.   
 
 Deployment having the merits,
 
- It can update the replicas with zero down time.
- Deployment controller contains deployment objects which can create new Replicas, remove old replicas excluding their resources and adopt it with the updated one.    