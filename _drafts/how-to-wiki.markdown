---
layout: post
title:  "Set up a Wiki with Mediawiki"
excerpt: "If you want to host your own wiki, this article will show you, how to deploy a wiki in 5 to 10 minutes"
categories: Tutorials
author: Sonny Alves Dias
tags: [ tutorials, devops, wiki, docker ]
---
Requirements: 
* [Docker](https://www.docker.com/){:target="_blank"} 
* A server with yourdomain.com already pointing at it
* 5-10 minutes

Everybody knows Wikipedia, but few know that Wikipedia is actually running on open source software. The Wikimedia Foundation develops his own wiki engine that they use for all their projects, including Wikipedia. This wiki engine is named [MediaWiki](https://en.wikipedia.org/wiki/MediaWiki){:target="_blank"}. That being said now, that's what we are going to use here to set up our own wiki :-)

First of all, you need a server with Docker installed on it. So obviously I would recommend a Linux server for that matter. As an example, Digital Ocean proposes an image with Docker preinstalled on Ubuntu so with a couple of clicks you can get a Droplet setup with Ubuntu and Docker ready-to-go. AWS and others have probably such equivalent images in their inventory too. 

If you have a look at the Docker hub, you will be able to find this Docker image in particular: [https://hub.docker.com/\_/mediawiki/](https://hub.docker.com\_/mediawiki/){:target="_blank"} This is the official docker image from the Wikimedia Foundation itself. This is definitely what we want to use. 

Considering your wiki project, you will decide if you need to use a MySQL-like database or use the default embedded SQLite. In our case we decided to use SQLite, which has the advantage of not requiring another container to run, but has the disadvantage of requiring the wiki to be in maintenance mode when doing a backup. 

So to deploy your MediaWiki with Docker, there's a little trick. First, create a folder wherever you want to store all the files related to the wiki. Then start the wiki, visit your wiki at http://yourdomain.com, do the setup, and download the LocalSettings.php generated for you. Finally, restart a new container with this LocalSettings.php and you are ready to go.

Here is the code I used:
```bash
# Create the folder
mkdir wiki; cd wiki

# Start the wiki setup 
docker run --name my-wiki -d |
	-v /wiki/data:/var/www/data  |
	-v /wiki/images:/var/www/html/images |
	-v /wiki/extensions:/var/www/html/extensions |
	mediawiki
```

Then like mentionned previously setup your MediaWiki and download the _LocalSettings.php_ at the end of the installation.

After that upload _LocalSettings.php_ into the wiki folder and run the following commands.

```bash
# Stop the container
docker stop my-wiki && docker rm my-wiki

# Setup the start script
echo docker run --name my-wiki -d -v /wiki/data:/var/www/data -v /wiki/images:/var/www/html/images -v /wiki/extensions:/var/www/html/extensions -v /wiki/LocalSettings.php:/var/www/html/LocalSettings.php --restart=always mediawiki > start.sh
chmod +x start.sh 
./start.sh
```

The command to start the container is kinda long so I suggest to save it in a `start.sh` in order to avoid to type it ever again. 

Voilà then just visit yourdomain.com and your wiki is ready to use. 

