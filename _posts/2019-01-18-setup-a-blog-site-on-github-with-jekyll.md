---
layout: post
title:  "Set up a blog on GitHub Pages with Jekyll"
excerpt: "It's never too late to make yourself a personal blog site, as long as you would like to spend sometime on some writings for someone else to take a look when they are searching about the things you are sharing. I am saying this to myself when I decided to setup this site and write this blog as the first post on my site."
author: Stefan Liu
categories: Tutorials
tags: [ tutorials, jekyll, blog ]
---

*Original article from [https://blog.devfans.io](https://blog.devfans.io/setup-a-blog-site-on-github-with-jekyll/){:target="_blank"}*

It’s never too late to make yourself a personal blog site, as long as you would like to spend some time to write for someone else to take a look when they are searching about the things you are sharing. I am saying this to myself when I decided to set up this site and write this blog as the first post on the site [https://blog.devfans.io](https://blog.devfans.io){:target="_blank"}.

#### Resources we would use

+ __GitHub Pages__: GitHub is an open platform for everyone whoever has the *open-source/resource* idea in his mind. It provides static web site serving service for free which is named as GitHub pages. <br>
More details here: [https://pages.github.com](https://pages.github.com){:target="_blank"}

+ __Jekyll__: Jekyll is the most popular tool to transform plain text into static websites and blogs. <br>
More details here: [https://jekyllrb.com](https://jekyllrb.com){:target="_blank"}

+ __A domain name (optional)__: You may like to have your own domain name like `https://blog.devfans.io`, but it's optional because GitHub provides you a free domain name as `your-user-name.github.io`.

#### Steps to setup it up

- If you get yourself a domain name for your site, go to the provider's website and create a `CNAME` record for your domain name with value as `your-gihtub-username.github.io`.

- Create a repo after you have your GitHub account, name it as `your-gihtub-username.github.io` and enable the GitHub pages, and configure the custom domain name if you have one. Also check the `enforce https` option is recommended.

- Clone a jekyll blog template you would like to choose (The one I am using is [https://github.com/wowthemesnet/mundana-theme-jekyll.git](https://github.com/wowthemesnet/mundana-theme-jekyll.git){:target="_blank"}).

- Config the site's name and author in `_config.yaml`, setup a comment tool (like [Disqus](https://disqus.com/){:target="_blank"}).

- Push the working copy to your GitHub repo, and it's up.


#### Sum up

I was mainly talking about the ideas to set up a personal blog site on GitHub Pages with Jekyll and didn't cover every detail during the process. If you want the detailed procedure, leave me a comment directly on my blog.