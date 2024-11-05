---
author: "Wren Howell"
title: "Practical Container Security"
date: 2024-10-25
description: "A little tidbit on container security"
tags: ["Container Security, Container Escape"]
thumbnail: https://www.eagleleasing.com/wp-content/uploads/2017/06/20ft-Storage-Container.jpg
---
Container security is exciting, and it is a very niche space to be. This post will build on the previous post about containers and look at common mistakes people make when deploying containers. The tricky thing about creating container detection is that it is hard to determine whether the end user is troubleshooting, not using the best practices, or exhibiting malicious behavior. The use cases will differ for each organization, so it will be up to the organization to determine the appropriate risk level, baseline their normal behavior, and decide what they want to monitor. 

Even though there are resources write about container best practices, many are not implemented because they are too time-consuming, expensive, or impractical. This blog post will focus on low-hanging container security risks that organizations can avoid and some potential detections for them.

Before diving into the technical layers of Docker security, it's essential to understand the container attack surface. Liz Rice and Aqua Security has a great diagram on container attack surface [here](https://krol3.github.io/container-security-checklist/). Even though it is not liston this blog post,  securing the host system is the most crucial element of container security because the container runs on top of the host operation system. If the host operation system is insecure, then it will not matter how much the containers are hardened, the whole infrastucture will be vulnerable. 

Continuing to use the Airbnb analogy from the last post, no matter how many bodyguards you hire at an Airbnb, if the building structure is damaged, the building is not secure. 

**Exposed Docker Socket**

Despite other alternatives to Docker, Docker is still the most popular common container management tool used to build, run, and manage containers. One of the common misconfigurations is exposure to the Docker Daemon Socket. A socket in Linux is an endpoint for sending or receiving data across a network. A socket communication medium that allows for programs to communicate with each other. A Docker Daemon Socket is a type of file that communicates between the Docker CLI and the Docker API. By default, the Docker API is exposed over a local UNIX socket, so that the Docker API is not exposed to the rest of the world. However, this default option can be changed to expose the Docker API externally to a specific TCP port. This is dangerous because it would allow any client with a specific IP address and port to execute commands. 

It is critical not to expose the Docker socket because even if it is not exposed to the external world, if it is found, threat actors can interact with it using tools like curl to run any command they want, essentially having a backdoor for accessing anything on the host. 

**Analogy of an Exposed Docker Socket**

A Docker socket file is like a keypad lock to the door to the Airbnb. The code for the door is reserved for the guests staying at the Airbnb. However, if the code is leaked to the Internet or passed around randomly to a group of strangers, Airbnb is no longer secure as anyone with the code to come into the Airbnb. 

**Examples in the Wild with Exposed Docker Socket**

Exposed Docker socket files are commonly used in Docker-in-Docker (DinD) setups within CI/CD pipelines, making it easier for engineers to build, test, and deploy applications. 

**Example of an Exposed Docker Socket** 

```bash
docker run -it --name REALLY-UNSAFE-CONTAINER -v /var/run/docker.sock:/var/run/docker.sock alpine
```

**Privileged Containers**

A privileged container is a container that has elevated privileges, which allows it to perform more actions than in a restricted environment. When a container is in privileged mode, it has the potential to gain the same access to the host system processes. A container in privileged mode can access mount host system resources, manage kernel resources, etc. Therefore, using privileged containers only when necessary is essential. 

**Analogy of Privileged Containers**

A privileged container is like a VIP guest at an Airbnb that has paid extra money for a special experience. Unlike regular guests, VIP guests can contact the host for special services like booking experiences or arranging maintenance. Like a VIP guest, a privileged container has broader permissions to perform actions that regular containers cannot do. 

**Example of a Privileged Container**

```bash
docker run --privileged -it  ubuntu:latest
```

**Excessive Capabilities**

Capabilities were mentioned in the previous post, but capabilities give the ability to grant privileges at a granular level. Giving a container additional capabilities is not inherently a bad thing --sometimes, additional capabilities are added for a container to run (in addition to the capabilities that are already included by default). A user can add many different types of capabilities to their container, but some capabilities, if combined with a privileged container, can lead to a container escape. 

**What is a Container Escape?**

A container escape is when a process or application running in a container gains access to resources outside of the container. Analogy of a container escape is when a prisoner breaks out of their cell and gets access to other resources in the prison. 

**An Example of Excessive Capabilities that Could Lead to Container Escape**

An example of how a container with additional capability can lead to a container escape is a proof of concept written by [Trail of Bits](https://blog.trailofbits.com/2019/07/19/understanding-docker-container-escapes/). This proof of concept abuses a feature in cgroup v1 notify on release. This feature notify_on release feature can trigger a container escape by allowing a script to execute when a cgroup becomes empty. An attacker can manipulate this process to run malicious code when it exits a cgroup that can access the host system. 

This proof-of-concept attack will not work on all containers. It will only work on containers with SYS_ADMIN capability, and the underlying host must use cgroup v1. 

**Read-Write Volume-Mounts**  

A volume mount is a way to provide persistent storage and share data between the host file system and a container. Volume mounts are used for data persistence, data sharing, and configuration. Containers are designed to be ephemeral, so the data disappears when you stop or remove the container. Developers usually need to use volume mounts on a container when creating applications requiring a database to store user info. 

However, if a developer mounts a sensitive host directory on a container in read-and-write mode, an attacker can escape from the container and onto the host. 

**Analogy of a Volume-Mount**

Not having a volume mount is like a friend who has all their photos on their iPhone without iCloud storage because they want to avoid paying an extra 10 dollars for more storage. Not paying for iCloud storage is only practical if they do not take pictures or have a history of breaking phones. Without iCloud storage, if they lose the phone, all their images will be deleted because the photos are only on their physical device.

On the other hand, having a volume mount is like a different friend who has adequate space on the iCloud. Even if they lose their iPhone, their pictures and videos will be recovered because their data is backed up to the cloud. 

**Example of a Sensitive Volume Mount**

```bash
docker run -v /etc:/etc --name sensitive_container -d nginx
```

**Potential Detections for the Techniques Outlined**

The easiest way to detect for the aforementioned container security vulerablities is to look for those commands  in the enironment.

- To look for exposed Docker Sockets look for files like yml or command lines that contain 
```bash /var/run/docker.sock```

- To look for containers with excessive capablities look for files like yml or command lines that contain 

```bash capabilities: add: "SYS_ADMIN" ``` 

- To look for containers that has a sensitive volume mount look for files like yml or command lines that contain 
```bash -v /etc ``` that also has a ```ro``` 

Keep in mind these are potential start on how to detect some of the behavior that was outlined on this post. I hope you enjoyed tidbit on containers!!

{{< css.inline >}}

<style>
.emojify {
	font-family: Apple Color Emoji, Segoe UI Emoji, NotoColorEmoji, Segoe UI Symbol, Android Emoji, EmojiSymbols;
	font-size: 2rem;
	vertical-align: middle;
}
@media screen and (max-width:650px) {
  .nowrap {
    display: block;
    margin: 25px 0;
  }
}
</style>

{{< /css.inline >}}
