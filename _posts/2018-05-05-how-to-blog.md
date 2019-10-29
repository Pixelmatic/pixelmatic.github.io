---
layout: post
title:  "[HOW-TO] Create a Blog"
excerpt: "If you want to host your own blog, this article will show you, how to deploy a blog in 5 to 10 minutes."
date:   2018-05-05 23:29:59 +0800
categories: devops blog docker
---
Requirements: 
* [Docker](https://www.docker.com/){:target="_blank"}
* A server with yourdomain.com already pointing at it
* 5-10 minutes

Like our previous article, we are going to use Docker and an official image from the Docker Hub. We will consider first that you are familiar with Docker and have it installed already on your server. 

So for your blog, we propose to use the blog system called Ghost. Based on Node.js, it is a modern and a very straightforward solution to anyone willing to start a blog. 
The Ghost developers also offer to host on their website, if you just want more info: [https://ghost.org/](https://ghost.org/){:target="_blank"} 

Now here is the process, first, we create a folder blog and a script _start.sh_. Then we just run the script. Et voila. :)

```bash
mkdir /blog && cd /blog
echo docker run -d --name ghost -p 80:2368  -e url=http://yourdomain.com -v /blog/content:/var/lib/ghost/content --restart=always ghost:alpine > start.sh
chmod +x start.sh
./start.sh
```

You can visit yourdomain.com and see your blog in action. 

*Note*: For those who want to use https (and I would strongly recommend you do), I will treat the subject on how to get an SSL certificate for free in a future article. 

