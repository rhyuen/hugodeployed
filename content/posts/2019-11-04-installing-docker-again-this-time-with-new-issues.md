---
layout: blog
title: Installing Docker Again.  This time with new issues!
date: 2019-11-04T07:30:36.911Z
thumbnail: /images/uploads/firstsprite.png
rating: 4
---
## Summary 
Installing Docker on a non-LTS version can result in there not being a tested version for your OS.  So either always get an LTS version or check to see if a supported version exists for your OS version.

## The Story


So, I downloaded Ubuntu 19.10, the non-LTS version unlike 19.04 (Disco), which is named 'Eoan' which one can figure out using the following:

```bash
$ lsb_release -cs  ### eoan
```
Initial thoughts are that the resulting output is an error; however, if one goes to the following wikipedia article [here](https://en.wikipedia.org/wiki/Ubuntu_version_history), Ubuntu 19.10 is listed as "Eoan Ermine" and Ubuntu 19.04 is listed as "Disco Dingo".  Regardless, on to the issue at hand.

As one follows the docs at Docker [here](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-engine---community-1):
```bash
$ sudo apt-get update
$ sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

> An error pops denoting that the specified repository doesn't exist.  The vaunted 404.

It seems, naturally, I am not the encounter this issue and that occurs fairly regularly. Someone else has already addressed the hard work [here](https://github.com/docker/for-linux/issues/833).

The initial solution I tried was re-running the last command with  'disco' isntead of '$(lsb_release -cs).  It doesn't work and returns with either the same or a similar error.  The issue likely stems from running the previous commands which modify files in `/etc/apt/` such as `sources.list`, `sources.list.d` and `sources.list.save`.  

It seems the solution is to remove all of the lines in the aforementioned files mentioning the version of docker that doesn't yet exist.  A user on StackOverflow mentions [here](https://askubuntu.com/a/989888) that one can run the following script to denote the lines in question: 
```bash
$grep -ne '^deb.*docker.*\\' /etc/apt/sources.list{,.d/*.list}
```
I didn't to use this solution.

Instead I cut and pasted the script mentioned [here](https://github.com/docker/for-linux/issues/833#issuecomment-544236041).  It is as follows: 

```bash
$ wget "https://download.docker.com/linux/ubuntu/dists/disco/pool/stable/amd64/containerd.io_1.2.6-3_amd64.deb"
$ wget "https://download.docker.com/linux/ubuntu/dists/disco/pool/stable/amd64/docker-ce-cli_19.03.3~3-0~ubuntu-disco_amd64.deb"
$ wget "https://download.docker.com/linux/ubuntu/dists/disco/pool/stable/amd64/docker-ce_19.03.3~3-0~ubuntu-disco_amd64.deb"
$ sudo dpkg -i "containerd.io_1.2.6-3_amd64.deb"
$ sudo dpkg -i "docker-ce-cli_19.03.3~3-0~ubuntu-disco_amd64.deb"
$ sudo dpkg -i "docker-ce_19.03.3~3-0~ubuntu-disco_amd64.deb"
```

I initially didn't think it would just execute right away upon pasting into the terminal.  However, that is what it did.  Seeing as how supposedly reponsible individuals are not merely just supposed to run code written by strangers directly into a terminal with admin priveleges, I at least verified that the files existed at the docker url [here](https://download.docker.com/linux/ubuntu/dists/disco/pool/stable/amd64). Slightly less irresponsible but still terrible.  All the files mentioned in the script exist at the parent URL.  Similar directions are also mentioned in the official Docker Documention [here](https://docs.docker.com/install/linux/docker-ce/#install-from-a-package) though it isn't quite as convenient as in the github post.

The end result is that it works.

And to run docker as a non-root user the following is required as mentioned in the 'linux post-installation options` denoted [here](https://docs.docker.com/install/linux/linux-postinstall/).

```bash
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
```

### Code (assuming everything works and nothing goes wrong) 
```bash
$ sudo apt-get update
$ sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
```
