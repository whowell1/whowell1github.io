---
author: "Wren Howell"
title: "The Kubernetes Threats 2024"
date: 2025-04-10
description: "k8"
tags: ["K8, threats"]
thumbnail: https://i.imgur.com/0HhNox3.png
---

Kubernetes is a technology that most people and most organizations do not understand. There is a lot of "deploy and hope" in most organizations. Kubernetes deployment is messy, and Kubernetes has a lot of moving parts that make it difficult to understand. So in this post, I want to breakdown the essential parts of Kubernetes.

However, before understanding the essential parts of Kubernetes are, we need to understand what Kubernetes is. Kubernetes, often abbreviated as k8, is an is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. 

So what does this mean and what problem did it solve?

When a developer deployed an app on a container, the developer had to manually start, stop, and manage them across multiple machines. For example, is an application needed more memory to run, a developer had to stop the container, increase the memory, and then restart manually. For a small number of containers this might be okay, but this quickly becomes unmanageable when there are hundrends of containers that developers that to manage. Kubernetes was a technology developed by Google to help automate this process. 

Kubernetes Architecture 

The control node is the brain of the Kubernetes. 
It consists of 
- API Server: This is the API that runs the Kubernetes API and where all the communication happens
- etcd: This is the database that stores the state of the cluster 
- Scheduler: This is the process that watches what runs on Kubernetes. 

Worker Node

This is a virtual machine that each pod runs on. A worker node has a 

- Kubelet: This is the agent that talks back to the K8 control plane
- KubeProxy: It manages networking and service discovery. 
- Container Runtime: Kubernetes supports multiple runtimes, but the default is CRI-O

What is a pod?
- Is the smallest unit of Kubernetes that can contain one or more containers. 

This all can be a little confusing so lets break it down in simplier terms using a airport as a example. 

The airport management staff and the air traffic control is like K9's control plane, it is responsible for organizing flights, scheduling, and maintaining overall operations of a airport. 

- The control tower is like the API server, it recieves flight plans, coordiantes with planes to give the pilots instructions on when to land, and take off. 
- The Flight Scheduler is like the scheduler in the Kubernetes, it assigns the gates and runways for each flight. 
- The flight database is like the etcd, it contains all the scheudles, aircraft status of the flights. 

A worker node is where all the action happens. Each worker node is like a terminal or runaway, where flights arrive, depart, and park. 

- The kubelet is like the flight attendents that ensures the passengers are following instructions so they can fly safely
- The engine, the wings, and the wheels of the engine like the container runtimes, tools that ensure planes can fly safely. 
- The staff at the airport at the counters that help you with baggage are like the kube proxy, they handle the communication between services. 

When talking about Kubernetes, there are different methods of deployments. They are managed, unmanaged, and custom Kubernetes that have the following:

Mananged Kubernetes

- Managed Kubernetes are Kubernetes instances that are managed by a cloud service provider like GSP, Azure, or AWS. In managed clusters, the cloud provider configures, provisions, and maintains the k8 clusters. This type of deployment allows the organization to leave the updating, infrastructure provisioning, and management to the cloud provider. 

Unmanaged Kubernetes Clusters 

- In unmanaged clusters, the user is in charge of installing, deploying, and operating Kubernetes environment or on the infrastructure the user controls. The user/organization is responsible for everything that allows them to have more control in this environment. 


Hybrid Kubernetes Clusters

- This is a type of deployment of k8 where there is a combination of using on-prem serveres, private cloud, and public cloud providers. 

Kubernetes Attacks

- Kubernetes attacks or compromises usually begin at a pod level where a threat actor compromised the application running the pod, a threat actor was able to phish a person who had access to a pod, or where a threat actor was able to escalate privledges on a pod.



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
{{ $image := $resource.Fit "600x400" }}
</style>

{{< /css.inline >}}
