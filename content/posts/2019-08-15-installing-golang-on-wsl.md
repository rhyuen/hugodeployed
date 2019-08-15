---
layout: blog
title: Installing Golang on WSL
date: 2019-08-15T10:51:24.357Z
thumbnail: /images/uploads/scieworld.jpg
rating: 5
---
There isn't that much in terms of direction for installing stuff on WSL which is linux-y with Microsoft Windows quirks.  Hopefully this post makes it such that there is slightly more direction on the matter.  I read through this [post](https://sal.as/post/install-golan-on-wsl/) and felt that it was quite helpful. I also tried the linux steps from the golang.org site [(link)](https://golang.org/doc/install?download=go1.12.8.linux-amd64.tar.gz).

Note, desite having a Windows Host, I am running WSL and downloading the Linux version of Golang.

My first attempt at things seemed to go alright.

1.) I went to [source](https://golang.org/doc/install?download=go1.12.8.linux-amd64.tar.gz) to grab the archive and followed the steps that followed the prompt.

2.) 
```bash 
$ tar -C /usr/local/ -xzf go1.12.8.linux-amd64.tar.gz
$ export PATH=$PATH:/usr/local/go/bin
$ source $HOME/.profile
```

3.) Run `go version` and things work out.  Close the terminal window

Things seem to have gone quite well.  Sadly, when I opened `Windows Terminal` again and typed `go version` .  Golang was nowhere to be found.  Run the above steps again because sometimes things go wrong. Once again confirm that the install works and run `go version` again.  It works.  Close the terminal and open it again.  Type `go version`.  Repeat error of not being found again.

Follow the steps at the [link](https://sal.as/post/install-golan-on-wsl/) listed above (not the golang.org one).  They're similar to the golang.org docs.

When I get to the 

```bash
$ sudo mv go /usr/local 
```
I get a weird error that says /usr/local/go is not an empty directory or something. So I get the feeling that maybe I should in `/usr/local` and see if `go` is there.  Turns out, it is.  I guess the earlier golang.org steps worked but the editing of the `$HOME/.profile` didn't work out.  In case it isn't obvious I am not awesome with bash and don't have a great handle on how all the .(appname)rc files work.

I ended up using the export paths listed in the link and appended them to the bottom of my `.bashrc` file.
```bash
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

I ran $ source ~/.bashrc and ran `go version`. It worked.

I closed the terminal, opened it again and ran `go version`.  It worked.


I'm hoping the below works when I inevitably refer to this in the future.  
I have NOT tested the below.  So if you're not me you probably should run the following.  Even if you're me, you probably shouldn't run the following.

```bash
$ sudo tar -C /usr/local/ -xzf go1.12.8.linux-amd64.tar.gz
$ echo 'export GOROOT=/usr/local/go' >> ~/.bashrc
$ echo 'export GOROOT=/$HOME/go' >> ~/.bashrc
$ echo 'export PATH=$GOPATH/bin:$GOROOT/bin:$PATH' >> ~/.bashrc
$ source ~/.bashrc
```

