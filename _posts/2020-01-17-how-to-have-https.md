---
layout: post
title:  "How to have HTTPS on my website for free"
excerpt: "Securing his own website is pretty easy now thanks to Certbot, check how in the article"
categories: Tutorials
author: Sonny Alves Dias
tags: [ tutorials, web, devops ]
---

Once you have your website running well on HTTP, you must activate HTTPS. And that for several reasons: 

* **Security** 
With HTTP the communications with the webserver are not encrypted so, for example, you log in on that server, a hacker could potentially capture your communication and read your password.

* **SEO** 
Google and others nowadays list in priority the HTTPS website, if you only have HTTP your website will be at the bottom of the list. 

* **Image** 
This is maybe something we may underestimate, but nowadays tech-savvy people are aware of security measures on the web. HTTPS being one of the most important measures to take to secure a website, it will increase your credibility to your audience. 

Fortunately, this is pretty easy nowadays, there are a couple of solutions to generate an SSL certificate for your website easily like [ZeroSSL](https://zerossl.com/){:target="_blank"} but here we are going to introduce [Certbot](https://certbot.eff.org/){:target="_blank"}.

Certbot can generate certificates recognized by all modern browsers. It generates certificates with 3 months validity maximum, but you can renew for 3 months as long as you want. They started to offer wildcard certificates also recently. 

Here is an example of how to use Certbot if you are using Nginx om Ubuntu 16.04. 

First of all, once Nginx is installed, your server may have a similar definition.
```
server {
    server_name yourdomain.com;
    listen 80;
    
    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
}
```

Then just follow the instructions from the Certbot website:

```
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository universe
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt-get update
$ sudo apt-get install certbot python-certbot-nginx 
```

Finally, just run: 

```
sudo certbot --nginx
```

Certbot will automatically detect your domain (defined in `server_name`) and propose to generate an SSL for it. During the process, it asks if you want to force visitors to use HTTPS by redirecting people arriving on HTTP to HTTPS. I strongly recommend to activate it. 

Et voila, your website is protected for the next 3 months. 

One last thing, if you want to have an automatic renewal of this certificate you can schedule a cronjob. Add these lines to your list as a superuser (`sudo crontab -e`).

```
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/opt/aws/bin:/root/bin
0 16 * * * certbot renew
0 4  * * * certbot renew
```

Here we are doing the verification twice every day to make sure the certificate will be renewed without any issue on the expiration day. 