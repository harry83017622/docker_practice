# **docker_practice**

## **Install**
This is a tutorial to simply walk through basic docker concepts and commands. First of all, please **Install Docker** by get started at https://docs.docker.com/get-docker/

## **Check version**
Please verify your installation by checking your docker version.
```docker
docker version
```
![image](/src/dockerversion.jpg)  

If there is no error raised, you are on the right track so far. We are going to write our first dockerfile soon.

## **Dockerfile**
Please clone this repo or use one of your favoriate editor (vim, notepad++, vscode, etc.) to create and open the dockerfile w/o filename extension. In my case, I used vscode. Then, you would see a cute whale icon before your Dockerfile.  

<div align=center><img width="300" height="40" src="https://github.com/harry83017622/docker_practice/blob/master/src/dockerfileicon.jpg"/>
  

Let's take a look at the dockerfile in the relative path **docker_practice/**.
```dockerfile
FROM ubuntu:16.04

# RUN apt-get update && apt-get install -y --no-install-recommends \
#     python3.5 \
#     python3-pip \
```

Before we actually build an image. Let's run 
```docker
docker images
```
to see if there is any images that have already existed in our environment.
<div align=center><img width="400" height="100" src="https://github.com/harry83017622/docker_practice/blob/master/src/dockerimages.jpg"/>
It shows that we don't have any image now. Then, we build an image use the command.  

```docker
docker build -t test_image_v1 .
```
<div align=center><img width="600" height="150" src="https://github.com/harry83017622/docker_practice/blob/master/src/dockerbuild.jpg"/>

Then, let's check images again.  

<div align=center><img width="450" height="80" src="https://github.com/harry83017622/docker_practice/blob/master/src/dockerimages_v2.jpg"/>
The result shows that we successfully build an image. We can build a container using this image now. Like what we did before, let us check existed containers in our environments.  

```
docker ps -a
```
<div align=center><img width="450" height="60" src="https://github.com/harry83017622/docker_practice/blob/master/src/dockerps_a_v1.jpg"/>
It shows that we don't have any container for now. Run the following command to build container:  

```docker
docker run -itd --name test_container_v1 be2
```
<div align=center><img width="450" height="60" src="https://github.com/harry83017622/docker_practice/blob/master/src/dockerrun_v1.jpg"/>
  
And check container now.

<div align=center><img width="650" height="80" src="https://github.com/harry83017622/docker_practice/blob/master/src/dockerps_a_v2.jpg"/>

We successfully build and start our container now. We can entry it using:
```docker
docker exec -it 92a bin/bash
```
<div align=center><img width="500" height="40" src="https://github.com/harry83017622/docker_practice/blob/master/src/dockerexec_v1.jpg"/>
We are now in our docker container env. 

```linux
cat /etc/os-release
```
<div align=center><img width="500" height="200" src="https://github.com/harry83017622/docker_practice/blob/master/src/checkubuntuversion.jpg"/>

However, if you execute python now in this container, you would raise an error. The reason is because we didn't install python in our docker image. We can now use apt-get to install python. But, it is not the spirit of docker (auto-set env). We can use dockerfile to solve this problem by just uncomment line #3-5.
Exit the container by Ctrl+d and open the editor to change dockerfile.
```dockerfile
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y --no-install-recommends \
    python3.6 \
    python3-pip \
```
Save it and build the image again.

```docker
docker build -t test_image_v2 .
```
<div align=center><img width="600" height="180" src="https://github.com/harry83017622/docker_practice/blob/master/src/dockerbuild_v2.jpg"/>

We finished building the image based on ubuntu:16 including python3.5 env.

<div align=center><img width="400" height="100" src="https://github.com/harry83017622/docker_practice/blob/master/src/dockerimages_v3.jpg"/>

We build the second container using new the new image.

<div align=center><img width="500" height="100" src="https://github.com/harry83017622/docker_practice/blob/master/src/dockerrun_v2.jpg"/>

we can now execute the new container and use python now.

<div align=center><img width="500" height="100" src="https://github.com/harry83017622/docker_practice/blob/master/src/dockerexec_v2.jpg"/>

So far, we now go through all docker flows.