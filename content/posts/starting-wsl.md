---
title: "Starting Wsl"
description: "linux on the windows"
date: 2019-06-13T19:33:31-07:00
draft: false
---

So, I finally started using `WSL` or Windows Subsystem for Linux.  The reason being that I tried to get nvm for windows to work out by deleting my original installs of Node and then setting up nvm for windows but I think I missed a spot and couldn't find out which spot I missed.  As a result, I am unsure of the version of Node that my `path` refers to.  As such, there are certain things that don't really work in my cmd prompt sessions.

Being one to make less than well researched designs, I figured lets give WSL an honest try.  I have some serious reservations on how the file system thing works with respect to how linux files and windows files intermingle.  However, I guess I'll just figure it out by suffering the hard way.  That's most accomdating of learning, right?

On to finding the directions.

# Finding the directions

To be honest, I wasn't entirely sure which directions/docs to use to setup on it.  I settled on the Linux ones.
The link I used is as follows: [Source](https://github.com/nvm-sh/nvm).

# The Directions

The directions I used were as follows: 

```bash curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash ```

You get a prompt at the end to tell you to do additional actions or you can exit and restart the terminal.  I opted for the latter.  

> I had serious reservations about executing an arbitrary bash script on the internet but remember, jumping in 'head-first'.  That's not an excuse but verifying for security purposes always leads me to putting the task off.

# Verification of Install

> ```bash command -v nvm```

# Installing Node 

To install latest
> ```bash nvm install node```


Things panned out alright thus far.  
