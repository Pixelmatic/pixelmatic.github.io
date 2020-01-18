---
layout: post
title:  "Build an online store without dealing with WordPress unreliability"
excerpt: "The couple WordPress and WooCommerce have been for too long the favorite solution to deploy quickly an online shop and start making revenue. Now every developer who encountered WordPress knows its many drawbacks. In this article, we will explain how we overcame WordPress's unreliability by turning it basically into a backend service. "
categories: Articles
author: Lawrence Zhao, Sonny Alves Dias
tags: [ articles, wordpress, woocommerce, devops, web ]
---

The couple WordPress and WooCommerce have been for too long the favorite solution to deploy quickly an online shop and start making revenue. Now every developer who encountered WordPress knows its many drawbacks. In this article, we will explain how we overcame WordPress's unreliability by turning it basically into a backend service. 

## First of all why WordPress is so popular?

* WordPress is **easy to deploy**, there are plenty of hosting solution that offers WordPress directly but also PHP hosting are still very commonly available, i.e. [wordpress.com](wordpress.com){:target="_blank"}, [DreamHost](https://www.dreamhost.com/wordpress/){:target="_blank"}, [BlueHost](https://www.bluehost.com/wordpress/wordpress-hosting){:target="_blank"}, etc.
* There are **a lot of plugins available**, and you can develop your plugin as well.
* There are **many pretty good looking themes**.
* It is **user-friendly**, especially to non-technical people.
* It has a **huge community** and numerous learning resources online.

## Then what's the problem with WordPress?

His popularity also brought weaknesses: 

- His huge community, mostly composed of non-technical users, generated a **huge amount** of non-official learning **resources** that are either **outdated or of poor quality**.

 [//]: <> (a lot of security holes because these users may not apply security patches to their WordPress regularly)
 
 - It also attracted **a lot of malicious and scammy developers** to make their own plugins polluting the plugins market. 

On a technical side:

- WordPress is **too flexible** in the sense that to implement something it can be done on different layers: in the PHP source code, in the WordPress page/post editor, or in the theme configuration. It leads non-technical users to not adopt clear conventions and let them try out different tricks here and there resulting in a very hacky usage of the CMS. 

- WordPress is also **unreliable** because of how updates are conducted, plugins and themes are simply overwritten thus losing any local changes (generally tailored-changes made to customize plugins and themes).
To be precise, WordPress has a child theme system that allows defining changes that will be applied on top of a parent that helps to prevent some of the local changes to be overwritten. But it is not well integrated or either user-friendly.
For webmasters, especially amateur ones, it is too risky to update plugins, themes, and WordPress itself because they are afraid of losing their changes and/or even break their entire website. Hence WordPress websites are de facto never updated.

## How to overcome the unreliability of WordPress?

Let's imagine we could use WordPress and WooCommerce for what they worth only which are a blog system and an online store system. 
The first thing we probably want to do is to remove the risks that are the plugins, and only install the minimum, WooCommerce. 
The second thing we want to do is to get rid of the themes too. To do that we started to look at Headless WordPress and found out about the WordPress API and the WooCommerce API. 

### WordPress API

WordPress, since its version `4.7.0` (released in December 2016), offers a RESTful API  that is to say 13 years after its first release in 2003 and only 3 years ago from the time of the writing of this article. 

The API allows interactions with WordPress using JSON (JavaScript Object Notation) format only. While for requesting data from it, it does not require authentication if you wish to edit, create, or delete information you will need to authenticate. It is worth noting that WordPress only supports Cookie Authentication natively, but some plugins allow for more types. 

The  consumption of the API is pretty straight-forward and allows you to retrieve any data pretty easily. The root endpoint is mounted on `/wp-json/`. From there you will be able to see all the available sub-endpoints. 
But let's dig into some examples:

- To retrieve the list of posts (articles) on your blog you can run a GET request at the endpoint `/wp-json/wp/v2/posts/` you will then receive the first page of the posts in JSON format. Complete example details are available here: [https://developer.wordpress.org/rest-api/reference/posts/#list-posts](https://developer.wordpress.org/rest-api/reference/posts/#list-posts){:target="_blank"}
- To retrieve a media that was used in a post you can run a GET request against the endpoint `/wp-json/wp/v2/media/<id>`, replace `<id>` by the actual id of the media. Complete example details are available here: [https://developer.wordpress.org/rest-api/reference/media/#retrieve-a-media-item](https://developer.wordpress.org/rest-api/reference/media/#retrieve-a-media-item){:target="_blank"}
- For more examples and details, the official documentation for the WordPress REST API is available at that address: [https://developer.wordpress.org/rest-api/](https://developer.wordpress.org/rest-api/){:target="_blank"}

### WooCommerce API

WooCoomerce has been offering a RESTful API to its users for a longer time than WordPress. The first WooCommerce API was released with WooCommerce `2.1.0` in February 2014 which is almost three years before WordPress' REST API.

It is more commonly used. For example, when you set up your logistics with ShipBob they will use the API to retrieve your shop orders automatically. 

It is important to note that the original WooCommerce API after several updates has been deprecated and relabeled Legacy API. WooCommerce decided to fully rework their API to extend the WordPress API directly after the release of the latter. 

We recommend to use the latest version which is at the time of this article is the WooCommerce API v3 (not the Legacy one but the current one).

When using the API whether the Legacy or the current one, you need to create first an API token in the settings of WooCommerce steps to follow are described here: [https://docs.woocommerce.com/document/woocommerce-rest-api/](https://docs.woocommerce.com/document/woocommerce-rest-api/){:target="_blank"}

Then to find out how to use the tokens to authenticate please go here: [https://woocommerce.github.io/woocommerce-rest-api-docs/#authentication](https://woocommerce.github.io/woocommerce-rest-api-docs/#authentication){:target="_blank"}

Finally here are some examples: 
- To create an order, you can run a POST request against that endpoint `/wp-json/wc/v3/orders` with a JSON object describing your order. Complete example details are available here: [https://woocommerce.github.io/woocommerce-rest-api-docs/#create-an-order](https://woocommerce.github.io/woocommerce-rest-api-docs/#create-an-order){:target="_blank"}
- To retrieve the list of products, you can run a GET request against that endpoint `/wp-json/wc/v3/products`. Complete example details are available here: [https://woocommerce.github.io/woocommerce-rest-api-docs/#list-all-products](https://woocommerce.github.io/woocommerce-rest-api-docs/#list-all-products){:target="_blank"}
- For more examples and details, the official documentation for the WooCommerce REST API is available at that address: [https://woocommerce.github.io/woocommerce-rest-api-docs/#introduction](https://woocommerce.github.io/woocommerce-rest-api-docs/#introduction){:target="_blank"}

### The next step

Now that we know how to use WordPress API and WooCommerce API, there are two things we need to consider:

* WooCommerce API needs authentication, so how are we going to keep our API tokens secret?
* And by using only the API, we are cutting ourselves from the payment process of WooCommerce. It means we will have to process payments ourselves outside of WordPress/WooCommerce.

This is why we went with the architecture below:

![Muted Wordpress](/assets/posts/muted-wordpress/architecture_wordpress_muted.svg)

- The front-end is running an Angular app written in Typescript.
- The middleware is a Node.js app written in Typescript, it holds the API tokens and implements the necessary things for processing payments too, for example, we usually implement [Stripe](https://stripe.com/docs/payments/accept-a-payment){:target="_blank"} and [GloBee](https://globee.com/docs/payment-api/v1){:target="_blank"}.
- The back-end and back-office is our WordPress.
- The CDN and storage are respectively running on AWS CloudFront and AWS S3.

It means that with that architecture when we want:

- To post an article, we add a post in WordPress, and we retrieve it through the WordPress API via our middleware,
- To host a picture, we simply upload it into WordPress media, and retrieve it with the CDN link,
- To do some changes in some parts of our website, we edit a WordPress page and retrieve the content of the page dynamically through the WordPress API via our middleware,
- To add a product, we simply add it into WooCommerce, 
- ...

<span style="text-decoration: underline;">Note</span> To automate the upload of the media to S3 in WordPress we installed the plugin [WP Offload Media Lite](https://wordpress.org/plugins/amazon-s3-and-cloudfront/){:target="_blank"}. Making the total count of our plugins installed into WordPress to only two: _WooCommerce_ and _WP Offload Media Lite_.


## Difficulties Encountered

- The WordPress API is slow: 
[https://stackoverflow.com/questions/45421976/wordpress-rest-api-slow-response-time/45425091#45425091](https://stackoverflow.com/questions/45421976/wordpress-rest-api-slow-response-time/45425091#45425091){:target="_blank"}
Though a plugin seems to help for that, by caching answers from the API:
[https://wordpress.org/plugins/wp-rest-cache/](https://wordpress.org/plugins/wp-rest-cache/){:target="_blank"} (We haven't tested it yet).

 [//]: <> (- Under special circumstances, you may want to register custom endpoint [https://developer.wordpress.org/rest-api/extending-the-rest-api/adding-custom-endpoints/](https://developer.wordpress.org/rest-api/extending-the-rest-api/adding-custom-endpoints/){:target="_blank"})

- To keep WordPress fully hidden behind our middleware (and avoid curious eyes), we had to filter all the links returned by WordPress to make sure they either use the CDN, use a vetted domain, or simply don't appear in the API calls answers. For that, the plugin _WP Offload Media Lite_ helps a lot because it updates every media link to use the CDN. 


## Final Thoughts

For us at Pixelmatic, to be able to fully customize the front-end as we want, while also keeping our website more secure is a major win for us. Admittedly the infrastructure needs are bigger but the maintainability and stability in the long term are higher. 