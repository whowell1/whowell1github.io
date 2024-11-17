---
author: "Wren Howell"
title: "Using ELK to do DFIR at scale Part 1"
date: 2024-11-10
description: "DFIR at Scale"
tags: ["Elk, DFIR, DFIR at scale"]
thumbnail: https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Jasper.Wapiti-Hirsch.P1033401.jpg/800px-Jasper.Wapiti-Hirsch.P1033401.jpg
---
One major challenge DFIR analysts face is analyzing infected machines at scale. Imagine there are four infected hosts. For the sake of this example, let's say an analyst needs to review artifacts like the NTUSER.DAT file, browser history, and multiple event logs. An analyst can use traditional tools like grep, PhiSearch, or Timeline Explorer can help sift through common artifacts, but manually combing through each log file with these tools is time-consuming and these traditional tools do not have a visual aid.

When a colleague suggested SOF-ELK as a solution, it immediately stood out as a perfect fit. [SOF-ELK](https://github.com/philhagen/sof-elk), created by Phil Hagen, is a forensic tool designed to streamline and accelerate log analysis and digital forensic investigations. It leverages the power of Elasticsearch, Logstash, and Kibana to provide an intuitive and efficient analysis experience. This implementation is dockerized, making it well-suited for resource-constrained environments.

 **Tools Used**

- Podman and podman desktop
- docker-elk
- homebrew (package manager for Mac)

**Explaination of tool choices**

I wanted this to be a quick, free and easy step up that is compatiable with different operating systems. Docker Desktop also started charging for organizations that are bigger than 500+ people. Podman is a free, open source alternative and most of the commands mirror docker. 

This verison of docker-elk using elastic version 7, that is easier to set up. These artifacts will only be used locally for analysis so additional security features that comes with verison 8 is optional. 

**Things to keep in mind**

The container that runs kibana, elastic search, and logstash need to have enough memory to run. Otherwise it will one of the dependencies will die. 

Figuring out what logs to ingest will be important too. The logs will have to be mapped to elastic search schema. Part 2 will have some demo logs from Crowdstrike that will be converted to elasic search schem

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
