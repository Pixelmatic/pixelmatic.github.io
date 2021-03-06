---
layout: post
title:  "Set up a blog with Ghost"
excerpt: "If you want to host your own blog, this article will show you, how to deploy a blog with Ghost in 5 to 10 minutes."
categories: Tutorials
author: Sonny Alves Dias
tags: [ tutorials, devops, blog, docker, ghost ]
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

*Note*: For those who want to use https (and I would strongly recommend you do), the subject is treated in the following article [How to have HTTPS on my website for free]({% post_url 2020-01-17-how-to-have-https %}). 

