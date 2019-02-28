# Docker Beginner Tutorial Step by Step

## Check docker version
#### <span style="color:red">Command:</span>  docker version

## Install image
#### <span style="color:red">Command:</span> *docker run <image_name>*
#### <span style="color:blue">Example:</span> *docker run busybox*
#### <span style="color:green">Output:</span>
```
Unable to find image 'busybox:latest' locally
latest: Pulling from library/busybox
697743189b6d: Pull complete
Digest: sha256:061ca9704a714ee3e8b80523ec720c64f6209ad3f97c0ff7cb9ec7d19f15149f
Status: Downloaded newer image for busybox:latest
```
##### docker run command can be divided into two parts
*docker run = docker create + docker start*
##### docker create = docker create <image_name>
##### <span style="color:red">Example:</span>  *docker create hello-world*
##### <span style="color:green">Output:</span>
```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete
Digest: sha256:2557e3c07ed1e38f26e389462d03ed943586f744621577a99efb77324b0fe535
Status: Downloaded newer image for hello-world:latest
d87a911122f1a86d23de1c1eadc8d2b3b622f18f8fe7b0635c2b5949b01948f8
```

##### docker start = docker start <container_id>
##### <span style="color:blue">Example:</span> *docker create -a d87a911122f1a86d23de1c1eadc8d2b3b622f18f8fe7b0635c2b5949b01948f8*
##### <span style="color:green">Output:</span>
```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete
Digest: sha256:2557e3c07ed1e38f26e389462d03ed943586f744621577a99efb77324b0fe535
Status: Downloaded newer image for hello-world:latest
d87a911122f1a86d23de1c1eadc8d2b3b622f18f8fe7b0635c2b5949b01948f8
```
### We can overide default command
#### <span style="color:red">Command:</span>  *docker run <image_name> <default_command>*
#### <span style="color:blue">Example:</span> *docker run busybox echo hi there*
#### Output: *hi there*
#### Example: *docker run busybox ls*
#### <span style="color:green">Output:</span> *show all the file directory of this image such as*
*bin
dev
etc
home
proc
root
sys
tmp
usr
var*

