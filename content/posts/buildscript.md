---
title: "Buildscript"
featured_image: "/images/sunrise.jpg"
date: 2019-06-05T16:01:40-07:00
draft: false
---

So, I've the `Hugo` quickstart a few times.  The thing is, I do it once and then leave it alone.  I feel bad for leaving the blog folder all alone and finally get the courage to try again.  Unforunately, at this I've forgotten all the commands, syntax and what they all do, hence why I've done it 'a few times'.  This post is an attempt to change that.  Hopefully it'll pan out.  I'm including a personal build script in `bash` that I never use (because Windows).

```bash
$ hugo new site latesthugoblog
$ cd latesthugoblog
$ git init
$ git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
$ echo 'theme = "ananke"' >> config.toml
$ hugo new posts/my-first-hugo-post-again.md
$ hugo server -D
```

Some notes, if you neglect the following commands: 
```bash
$ git init
$ git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
```

it will present you with an error and you won't be able to see anything when you go to `http://localhost:1313`.

Also, if you're on `Windows`, for the following line: 
```bash
$ echo 'theme = "ananke" >> config.toml
```
I just go to the file located in the `root` directory of the folder that the `hugo` cms generated and edit it with my text editor.