---
layout: blog
title: Things that worked out in NetlifyCMS
date: 2019-07-04T23:28:22.947Z
thumbnail: /images/uploads/scieworld.jpg
rating: 5
---
I mentioned in my previous [post](https://royu.netlify.com/posts/2019-07-04-netlifycms/) that I still had to 'kick the tires'.  

Here's some stuff that worked out.  I can login and logout successfully.  The changes made on the web GUI are committed to the Github repository.  Thus, I could successfully pull the updates via CLI:

> $ git pull origin master

Things that aren't working out or are weird 'quirks'.
1. Each post I create requires a 'Featured Image' be selected in the 'Admin' interface despite the aforementioned images being not-visible in blog.  
2. Similarly, a 'Rating Scale' is also required.
3. I made a change to one of my old posts (It was a link). I didn't see the results when a refreshed the page (Shift + F5, for force refresh). I suspect it may be a bug.
4. What functions as a 'New Post' button is called a 'New Blog1' button.  'Blog1' is the value of the `collections[0].label field.
