---
author: "Wren Howell"
title: "Investigating Suspicious Containers on Host" 
date: 2025-12-15
description: "Investigating Containers"
tags: ["Incident Response, Container Security"]
thumbnail: https://as1.ftcdn.net/jpg/07/22/57/22/1000_F_722572280_NEm2lcXDqeOowglTUdMtxwxPdQdnHW7r.jpg
---
# Triaging Malicious Containers: A Shai-Hulud Case Study

Supply chain compromises like Shai-Hulud are nightmares because remediation has to happen at every level of the affected machines. Even if remediation is done at the first tier, if it doesn't occur at every level after that, there is still a risk of compromise—especially when a popular tool like npm packages gets hit.

## What is Shai-Hulud 2.0?

Shai-Hulud 2.0 is a supply chain worm that targets the npm ecosystem by infecting legitimate packages with malicious code. Once a developer installs a compromised package, the worm steals sensitive credentials such as npm tokens, GitHub tokens, and cloud keys from local machines and CI/CD pipelines. It then uses those stolen credentials to automatically compromise and republish other packages—allowing it to propagate rapidly like a worm.

Many researchers have published IOCs associated with Shai-Hulud 2.0, and identifying them on hosts by looking up hashes is relatively trivial. But if the affected Shai-Hulud npm package is not on a traditional host (e.g., a container service deployed as a Service Principal), triaging looks a little different.

I've wanted to write a blog post on how to triage potentially malicious containers for a long time, so I'm using this Shai-Hulud incident to do so. This guide is a walkthrough on how to investigate potentially malicious containers using the IOCs from Shai-Hulud as a guide. This walkthrough assumes that the container is running on a host and is a Linux-based container.

## Important Distinctions

**Images vs. Containers:**
- **Images** are read-only templates that contain everything needed to run something. An image is like a recipe to make a cake.
- **Containers** are running instances of the image. The container is the actual cake.

Note: Throughout this guide, images and containers may be used interchangeably, but keep this distinction in mind.

## Step 1: Getting the Malicious Container from the Host to Your Analysis Machine

First, find the running containers on the host by using:

```bash
docker ps -a
```

This command lists all containers (both running and stopped). The `-a` flag shows all containers, not just running ones.

Once you've identified the container of interest, save its state into a `.tar` file:

```bash
docker export <container_id> -o malicious_container.tar
```

Or, if you want to save the image instead:

```bash
docker save -o malicious_image.tar <image_name>:<tag>
```

**Note:** `docker export` exports the container's filesystem, while `docker save` exports the image with all its layers and metadata. For forensic analysis, `docker save` is often preferred as it preserves more information.

## Step 2: Transfer the .tar File to Your Analysis Machine

Transfer the `.tar` file to your analysis machine. I use a EDR like Crowdstrike and Defender so all I do is download the file and unzip it onto my host. 

## Step 3: Load the Container/Image on Your Analysis Machine

Once the `.tar` file is on your analysis machine, load it:

If you used `docker save`:

```bash
docker load -i malicious_image.tar
```

If you used `docker export`, you'll need to import it as an image:

```bash
docker import malicious_container.tar malicious_container:analysis
```

## Step 4: Run the Container and Analyze

Now run the image in an isolated environment so you can analyze the files:

```bash
docker run -it --rm --network none <image_name>:<tag> /bin/bash
```

**Flags explained:**
- `-it`: Interactive terminal
- `--rm`: Automatically remove the container when it exits
- `--network none`: Isolate the container from the network (important for malware analysis)
- `/bin/bash`: Start a bash shell 

**Alternative: Analyze without running the container**

For safer analysis, you can also inspect the filesystem without actually running the container:

```bash
# Create a container from the image without starting it
docker create --name analysis_container <image_name>:<tag>

# Export the filesystem
docker export analysis_container -o filesystem.tar

# Extract and analyze
tar -xf filesystem.tar -C ./analysis_directory/

# Clean up
docker rm analysis_container
```

## Step 5: Look for Shai-Hulud IOCs

Now that you're in the shell of the container (or have extracted the filesystem), you can look for potential IOCs associated with the Shai-Hulud malware:

```bash
# Check for suspicious npm packages in node_modules
find / -name "malicious_node_modules" -type d 2>/dev/null


## Additional Forensic Steps when looking for compromised npm packages on a host

- **Inspect package.json files** for suspicious dependencies or install scripts
- **Review .npmrc files** for unexpected registry configurations
- **Review Docker image layers** to see when malicious code was introduced:

```bash
  docker history <image_name>:<tag>
```

## Conclusion

Supply chain attacks like Shai-Hulud demonstrate the importance of having proper incident response procedures for containerized environments. By following this methodology, security teams can effectively triage suspicious containers and identify compromised dependencies before they spread further through the environment.






















Supply Chain compromises like Sha-Halud are nightmare because remediation has to happen at every level of the affected machines. Even if remediation is done at the first tier, if remediation does not occur at every level after that, there is still a risk of compromise, espescially when a popular tool like npm packages get hit. 

Here is a basic summary what Sha-Hulud is:

- Shai-Hulud 2.0 is a supply chain worm that targets the npm  ecosystem by infecting legitimate packages with malicious code. Once a developer installs a compromised package, the worm steals sensitive credentials such as npm tokens, GitHub tokens, and cloud keys from local machines and CI/CD pipelines, then uses those stolen credentials to automatically compromise and republish other packages—allowing it to propagate rapidly like a worm.

Many researchers published IOC's associated with Shai-Hulud 2.0 and identifying them on hosts by looking up hashes is relatively trival. But if the affected Sha-Hulud npm package is not a traditional host (container service that is deployed in a Service Principal), triaging looks a little different. I also wanted to write a blog post on how to triage potential malicious containers for a long time, so I am taking this Sha-Hulud incident to do so. This guide is a walkthrough on how to investigate potential malicious containers, using the IOC's in the Sha-Hulud as a guide. This walkthrough also assumes that the container is running on a host and is Linux based container. 

Somethings to keep in mind:

- Images and containers will be used interchangeably but there is a distinct difference between the two

- - Images are a read-only template that contains everything that needs to run something. A image is the a recipe to make a cake

- - Containers is a running instance of the image. The container is the actual cake. 
 

1) Getting the malicious container from the host of interest to analysis machine:

- I wrote a explanation of containers previously, here. But before that find the running containers on the host by using 

``` docker ps -a

``` 

Once the containers of interest are found, the next step is to save the state of the container into a .tar file and transfering the file contexts in a investigative machine. Export the state of the container by running a 


```
``` 

Now that the container is saved as a .tar file, transfer it over to the analysis machine. 

Once that .tar file is on the analysis machine, the contexts of the file need to be loaded to the it by running a 

```
```

Now that the file is loaded, now the image needs to run so that you can analyze the files. Run the image by running a 


```
```

Now the the containers is running and you are in the shell of the container, you can look for the potential IOC's associated with the Sha-Hulud malware. 




There was a recent investigation involving Sha-Halud and there was a container that I wanted to investigate on a host. Even though the container was not malicious, it gave me a chance to brush up on my skills on investigating containers and so I wanted to write a blog post on it. 

Let's say there is an alert on a host that potentially has an container that is of interest. Assuming the host is running a Linux container and has Docker installed, the first step to figure out running container on the host of interest is to do a 

docker ps -a 

This is show a list of running containers on the host.

Once the containers are identified, the next step is to download  

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
