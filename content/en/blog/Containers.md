---
author: "Wren Howell"
title: "Understanding Containers and their underlying Technology "
date: 2024-02-26
description: "Containers Learning Journey"
tags: ["Containers, learning"]
thumbnail: https://cdn.shopify.com/s/files/1/0120/4849/8752/files/iStock-1284852950_480x480.jpg?v=1618857709
---
**Understanding Container Security**

Two years ago, I started on a journey to understand containers. In that journey, I dove deep into containers and here are the highlights of what I learned.

**Why are containers popular?**

The reason containers became popular is that with containers, developers could put their code in a box called a container and ship it without worrying about configuring the environment that runs their code. Before containers, developers would have to spend time setting up their environments so the code could run. There were a lot of "it works on my machine, but I don't know why it doesn't work on your machine" issues. 

**What is a container?**

A container is defined by OCI (Open Container Initiative), and from their definition, a standard container is an environment for executing processes with configurable resource limitations. In addition, containers must support these processes: create, start, kill, delete, and query state. 

**Translated in Simpler Terms**

This means that containers are places where you can run programs with constrained resources, and they should be able to do specific tasks like creating, starting, stopping, deleting, and checking the status of these programs.

**Why is the environment restricted?**

Since people who work in tech are most familiar with Docker containers which are Linux-based containers, I will explain how a Docker container can run programs in a constrained environment. 

A container is in a restricted environment because it shares the kernel with the underlying host. This allows the container to run on the same operating system as the host, unlike virtual machines where the VM DOES need a separate kernel. So, a good analogy would be going on a trip with a group of friends and their significant others for a birthday celebration. Instead of staying at a different hotel, everybody stays in an Airbnb that has two stories, a basement, and an extra cottage in the backyard. At an Airbnb, all the friends can share the same resources the house provides, like a bathroom and a kitchen. Some of the benefits of staying at the Airbnb instead of the hotel is that it is cheaper, it is easier to coordinate activities, and it is faster to get up and go.

In this case, renting an Airbnb would be a container, and going to a hotel would be a virtual machine as everybody will be under one roof and will share resources of the home. Just like if everybody stays at the Airbnb, it is faster to go places together, and cheaper than staying at a hotel, containers are much quicker to start up, less resource intensive than virtual machines. 

**What does it mean to run programs in a restricted environment?**

Continuing with the Airbnb analogy, just because everybody stays at the Airbnb and NOT in a hotel, everybody should be able to do everyday things that they do in a hotel. The mechanism in which containers allow programs to be run, start, kill, delete, and query state is provided by the underlying Linux technologies. These technologies are namespaces, capabilities, cgroups, and through mandatory access controls like SELinux or AppArmor, and finally through filters like seccomp. 

**What are namespaces?**

Namespaces are a feature in Linux that allows processes to have their own isolated view of system resources. Going back to the Airbnb analogy, each room represents a specific resource or aspect of the system, and namespaces are like partitions or sections within this house that provide isolation for different activities. Eight namespaces are currently supported by Docker: mount, PID, network, Cgroup, IPC, time, UTS, and user namespace. Each one serves an important function, but I want to highlight the mount, PID, time, and user namespaces. Each of these namespaces is explained in further detail in the Linux man-pages. 

Mount namespace: Picture this as a storage room for storing different items (files and directories). Just as the Airbnbn will have a central storage area, each room of the Airbnb will also have its own storage area as well with its own layout. For example, the basement and the cottage in the backyard will have different storage layouts, and the friend staying at the basement should not store their belongings in the cottage. In the same way, processes within a mount namespace have their own isolated view of the filesystem, with their own set of mounts and directories.

PID namespace: Imagine that at this Airbnb, there is going to be a huge party on the first floor and each room of the Airbnb is going to have a theme. Because the music is very loud in each room, only the people with the same theme can communicate with each other. In this analogy, a theme in the party represents a namespace. Just like how only people in the same theme can only communicate with each other, because processes within a PID namespace have unique process IDs, they cannot  or interact with processes outside their namespace.
  
Time: Imagine you have a habit of being late, so in your room, you set your clock 15 minutes earlier than the clock in the Airbnb's living room. Similarly, processes in this namespace can have different time settings than the underlying host. 


User Namespace: Consider this a room where you and your friends (users) in the house have their own keys and access privileges. Each person can access certain rooms based on their keys, but they can't access rooms they don't have keys for. To further break down the example, you will only have access to your room when you lock the door, not your friend's. Similarly, processes within a user namespace have their own isolated user and group IDs, separate from the IDs in the rest of the system.


Network: Imagine this as a basement in the Airbnb with its own utilities such as electricity, water, and internet connection. Each bathroom represents a namespace as each bathroom has isolated plumbing and lights that serve the needs of each friend. The flooding of one bathroom will not make the bathrooms in the Airbnb unusable. Similarly, processes within a network namespace have their own isolated network configuration, like network interfaces that provide security, resource management, and isolation for its processes. 


**What are capabilities?**

Capabilities give the ability to grant privileges at a granular level. Continuing with the Airbnb analogy, imagine if you had to ask the Airbnb host for every change you wanted to make during the stay, like adjusting to temperature or requesting the owner of Airbnb to see if you could invite additional friends over for dinner at Airbnb. This would take a long time and provide a frustrating experience, as you would have to wait until the host responds. From the host's perspective, they also want to give a great experience to their guests and not be bothered by every little change, but they want to protect their property by not having any rules. The decision to permit doing certain things would be up to the person's name on Airbnb as they will be the one responsible for the condition of the Airbnb. In this way, capabilities give the system granular control ability without being over-permissive.   

**What are Cgroups?**

Cgroups, short for "control groups," is a feature in the Linux kernel that allows you to manage and allocate system resources, such as CPU, memory, disk I/O, and network bandwidth, among groups of processes. Continuing with the Airbnb analogy, cgroups ensure that one friend or a couple of friends do not use all the water or electricity and are not inconvenient to other people. 
Most modern Linux operating systems utilize Cgroup2, but there could be both cgroup1 and cgroup2 on a host. Cgroup2 is a more advanced implementation of cgroup1 and has additional security controls that enable newer features like rootless containers. 

**What are mandatory access controls?**

Mandatory Access Control (MAC) is a security model used in Linux systems to restrict and control access to resources based on rules set by system administrators. A good analogy would be the strict Airbnb security policies on who can rent an Airbnb. Suppose Airbnb has a policy in the user agreement that a guest on an FBI watchlist cannot stay as a guest. In that case, it will not matter how famous or how much money the guest on the FBI watchlist is; the friend cannot stay. In this way, MAC sets strict rules about who can access what resources on a computer system. These rules are decided by administrators and are not negotiable, and these rules are enforced automatically. 

Depending on the operating system, the type of MAC control changes. Debian-derived systems have AppArmor by default, and Red Hat-based systems use SeLinux.

AppArmor creates a "profile" for each program, which contains the rules governing its behavior. These profiles restrict access to a number of resources, including files, network traffic, and Linux Capabilities.

Understanding AppArmor and SELinux Better with Airbnb Analogy
SELinux is like having strict rules and regulations enforced by the landlord for every aspect of the rental property. Each room has specific rules that guests have to follow , such as what they can touch and who they can interact with. These rules are rigidly enforced, ensuring a high level of security but leave little room for context.

On the other hand, AppArmor is more like having personalized security guards assigned to each guest. These guards closely monitor the activities of individual guests and intervene if they detect any suspicious behavior or if a guest tries to access restricted areas. The rules are tailored to each person’s behavior and can be adjusted more based on their specific circumstances. This approach provides a flexible and customizable security solution but requires more effort and resources to ensure optimal protection.

What is Seccomp? 

Seccomp, short for Secure Computing Mode, is a feature in the Linux kernel that allows you to restrict the system calls made by a process. Seccomp filters are rules or policies that define which system calls a process is allowed to make, limiting its ability to interact with the operating system. For example, when a process tries to make a system call, Seccomp checks it against the defined rules. If the system call is allowed by the rules, it is executed normally. However, if the system call is not permitted, Seccomp blocks it and prevents the system call from being executed.

In the Airbnb, Seccomp acts like a strict bouncer stationed at the property entrance. This bouncer has a defined list of allowed activities and behaviors for guests. When you arrive, the bouncer checks their ID against the list and only allows you to engage in defined and safe activities. Anything outside these approved activities is strictly prohibited, and the bouncer immediately intervenes to prevent it.

So, if one of your friends try to engage in any activity not on the approved list, like trying to access sensitive areas or performing potentially dangerous actions, the bouncer blocks them from doing so, ensuring that only safe and permitted actions are allowed within the Airbnb property.

In summary, Seccomp acts as a vigilant gatekeeper, restricting guests (or, in this case, processes) to only perform authorized and deemed safe activities, enhancing security within the Airbnb environment.




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