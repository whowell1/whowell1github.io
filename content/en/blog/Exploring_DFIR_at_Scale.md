---
author: "Wren Howell"
title: "Using ELK to do DFIR at scale Part 1"
date: 2024-11-10
description: "DFIR at Scale"
tags: ["Elk, DFIR, DFIR at scale"]
thumbnail: https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Jasper.Wapiti-Hirsch.P1033401.jpg/800px-Jasper.Wapiti-Hirsch.P1033401.jpg
---
One major challenge DFIR analysts face is analyzing infected machines at scale. Imagine four compromised hosts. For this example, an analyst needs to review artifacts like the NTUSER.DAT file, browser history, and various Windows event logs.

Traditional tools like grep, PhiSearch, or Timeline Explorer can help sift through these artifacts, but manually combing through each file is time-consuming. These tools also lack visual aids, which can slow down analysis and make pattern recognition harder.

When a colleague suggested SOF-ELK, it immediately stood out as a great solution. Created by Phil Hagen, SOF-ELK is a forensic-focused tool built to streamline and accelerate log analysis. It leverages the ELK stack (Elasticsearch, Logstash, and Kibana) to provide an intuitive and powerful interface for analyzing forensic data. Best of all, it’s dockerized—making it ideal for running in resource-constrained environments.

 **Tools Used**

- Podman & Podman Desktop
- docker-elk
- Homebrew (Mac package manager)


**Explaination of tool choices**

I wanted a quick, free, and easy setup that’s compatible across different operating systems. Podman is a free, open-source alternative to Docker, and most commands are Docker-compatible.

This version of docker-elk uses Elasticsearch 7, which is simpler to set up compared to version 8. Since these artifacts will be analyzed locally, the advanced security features in version 8 aren't necessary for this use case.


**Things to keep in mind**

Resource Usage: The containers running Kibana, Elasticsearch, and Logstash require enough memory. If resources are tight, one of the services may fail to start.

Log Mapping: Deciding what logs to ingest is important. These logs need to be mapped to the correct Elasticsearch schema. In Part 2, we’ll take sample logs from CrowdStrike and show how to convert them for ingestion and visualization.

**Installation steps**

1) Install homebrew [here](https://brew.sh)

or put this in terminal

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2) Install podman and podman desktop 

```bash
brew install podman && brew install podman-desktop
```

3) Download this github [repo](https://github.com/deviantony/docker-elk)

4) Go to the directory where the compose file is 

```bash
podman-compose up
```

5) After a couple of minutes or so, there should be a welcome to kibana page that should show up at http://localhost:5601

Stay tuned in for part two, where we will take some sample data from Crowdstrike, map them to elastic search and display the logs in our elastic search instance. 

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
