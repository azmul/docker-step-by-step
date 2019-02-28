# Docker Beginner Tutorial Step by Step

## Why use docker ?
##### Docker makes it really easy to install and run software without worring about setup and dependencies.
## Docker Ecosystem
> [Docker Client] [Docker Server] [Docker machine] [Docker images] [Docker Hub] [Docker Compose]
##### Docker is a platform or ecosystem around creating and running containers.
##### [Note: *When runnig docker in my computer technically running Linux virtual machine in my computer*]
## What is container and images ?
##### Image is a single file with all the dependencies and config required to run a program.
##### Container is instance of an image runs a program.
##### [Note: *Docker cli and Docker hub combines download Image*]
## Check docker version of your computer
#### Command: docker version
#### Output:
```
Client: Docker Engine - Community
 Version:           18.09.2
 API version:       1.39
 Go version:        go1.10.8
 Git commit:        6247962
 Built:             Sun Feb 10 04:12:39 2019
 OS/Arch:           darwin/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          18.09.2
  API version:      1.39 (minimum version 1.12)
  Go version:       go1.10.6
  Git commit:       6247962
  Built:            Sun Feb 10 04:13:06 2019
  OS/Arch:          linux/amd64
  Experimental:     true
```

## Install image
#### Command: *docker run <image_name>*
#### Example: *docker run busybox*
#### Output:
```
Unable to find image 'busybox:latest' locally
latest: Pulling from library/busybox
697743189b6d: Pull complete
Digest: sha256:061ca9704a714ee3e8b80523ec720c64f6209ad3f97c0ff7cb9ec7d19f15149f
Status: Downloaded newer image for busybox:latest
```
##### [Note: *To generate this image docker took the following steps*]
> [Docker Client] -> [Docker Server] -> [Image Cache] if not found then pull the *busybox* image from the docker hub 
##### docker run command can be divided into two parts
*docker run = docker create + docker start*
##### docker create = docker create <image_name>
##### Example: *docker create hello-world*
##### Output:
```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete
Digest: sha256:2557e3c07ed1e38f26e389462d03ed943586f744621577a99efb77324b0fe535
Status: Downloaded newer image for hello-world:latest
d87a911122f1a86d23de1c1eadc8d2b3b622f18f8fe7b0635c2b5949b01948f8
```

##### docker start = docker start <container_id>
##### Example: *docker create -a d87a911122f1a86d23de1c1eadc8d2b3b622f18f8fe7b0635c2b5949b01948f8*

## We can overide default command
#### Command: *docker run <image_name> <default_command>*
#### Example: *docker run busybox echo hi there*
#### Output: *hi there*
#### Example: *docker run busybox ls*
#### Output: *show all the file directory of this image such as*
```
bin
dev
etc
home
proc
root
sys
tmp
usr
var
```

## Containers command
#### To check list all containers ever created
#### Command: *docker ps --all*
#### Output: 
```
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS                         PORTS                    NAMES
c6f1310d15f4        busybox               "ls"                     24 minutes ago      Exited (0) 24 minutes ago                               thirsty_dijkstra
d87a911122f1        hello-world           "/hello"                 32 minutes ago      Exited (0) 28 minutes ago                               reverent_feiste
```
### To check all running containers
#### Command: *docker ps*
### Remove all stopped containers
#### Command: *docker system prune*
### Retrieving log outputs
#### Command: *docker logs <container_id>*
### Remove a  containers
#### Command: *docker rm <container_id>*
### Stopping containers
#### Command: *docker stop <container_id>* [Take 10 second to stop terminal signal]
#### Command: *docker kill <container_id>* [Instanlly kill terminal signal]

## Execute an additional command in a container
#### Command: *docker exec -it <container_id> command*
>docker [reference to the docker client]

>exec [runs another command]

>-it [allows us to provide input to the container]

>container_id [id of container]

>command [command to execute]
#### Example: *docker exec -it 60d8b59809e7 redis-cli*
#### Output
```
127.0.0.1:6379>
```
## Getting a command prompt in a container
#### Command: *docker exec -it <container_id> sh* 
#### Example: *docker exec -it 60d8b59809e7 sh*
#### [Note: *sh is command processor of shell*]
#### Output:

```
# cd /
# ls
bin  boot  data  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
# redis-cli
127.0.0.1:6379>
```
#### [Note: To exit type exit or ctrl+D]

## Build customs images through Docker server
#### Custom image means own application or own virtualization containers.

### How to make a custom image ?
#### Steps are 
> [Dockerfile] -> [Docker Clinet] -> [Docker Server] -> [Usable Image]
#### Here, *Dockerfile* means a configuration how our container should behave.

### Creating a Dockerfile flow below's steps
>1. Specify a base image

>2. Run some commands to install additional programs

>3. Specify a command to run on container startup.

#### Example: Now, We will create an image that runs redis-server. So create a floder and then create a dockerfile. Then types belows command.

```
FROM alpine
RUN apk add --update redis
CMD ["redis-server"]
```
#### Here details are


| Instruction telling Docker server what to do        | Argument to the instruction           | Description  |
| ------------- |:-------------:| -----:|
| FROM      | alpine | use an existing docker image as base |
| RUN      | apk add --update redis      |   Download and install a dependency |
| CMD | ["redis-server"]      |    tell the image what to do when it starts as a container |

#### To build this image run command is: *docker build .*
#### To run this image command is: *docker run <container_id>*

### Rebuilds with cache
##### [Note: *When we add some new instruction in a docker file docker download new dependency according to new instruction and takes other with cache. if we change docker instruction from upper and bottom then docker download all dependency newly*]

## Tagging an image
##### To build an image with a tag follow the below command
#### Command: *docker build -t <docker_id/><repo/project_name:latest>  .*
#### Example: *docker build -t azmul/redis:latest .*

## Project outline making a real project
##### Now we will make a nodejs web app into a docker container and will run from a browser. 

#### Steps are
> 1. Create nodejs web app

> 2. Create a Dockerfile

> 3. Build image from Dockerfile

>4. Run image from container

> 5. Connect to web app from a container

