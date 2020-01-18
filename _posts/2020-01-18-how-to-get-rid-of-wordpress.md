---
layout: post
title:  "Build an online store without dealing with WordPress unreliability"
excerpt: "The couple WordPress and WooCommerce has been for a long time the favorite solution for people to deploy quickly an online shop and start making revenue. 
Though every developer that encountered WordPress knows its many drawbacks."
categories: Articles
author: Lawrence Zhao, Sonny Alves Dias
tags: [ articles, wordpress, woocommerce, devops, web ]
---

The couple WordPress and WooCommerce have been for a long time the favorite solution for people to deploy quickly an online shop and start making revenue. 
Though every developer that encountered WordPress knows its many drawbacks.

## Why WordPress is so popular?

1. WordPress is easy to deploy, there are plenty of hosting solution that offers WordPress directly but also PHP hosting are still very commonly available, i.e.:
- [wordpress.com](wordpress.com){:target="_blank"}
- [DreamHost](https://www.dreamhost.com/wordpress/){:target="_blank"}
- [BlueHost](https://www.bluehost.com/wordpress/wordpress-hosting){:target="_blank"}
- etc.
2. There are a lot of plugins available, and you can develop your plugin as well
3. There are many pretty good looking themes 
4. Friendly to the non-technical person
5. A huge community and numerous learning resources online

## The problem with WordPress

His popularity is also one of his weaknesses because being friendly to non-technical people, generated a huge amount of non-official learning resources that are either outdated or of poor quality, a lot of security holes because these users may not apply security patches to their WordPress regularly, and also attracted a lot of beginner developers or malicious/scammy developers to make their own plugins diluting, even more, the plugins market. 

On a technical side, WordPress is too flexible in the sense that to implement something it can be done on different layers: in the PHP source code, in the WordPress dashboard, in the Theme configuration, making non-technical person not adopting conventions it allows them to try out different tricks here and there thus complexifying their website to the most. 

WordPress is also unreliable because of how updates are conducted, plugins and themes are simply overwritten when updating losing any local changes (made with the tricks applied here and there).
To be honest on the theme side, WordPress has a child theme system which allows to define changes that will be applied on top of a parent but first, it has never been well-integrated and neither well-promoted in their systems and second for a theme that is still actively being developed it will probably not be enough in the long run. 
The result is that for webmasters and website owners it becomes risky to update plugins, themes, and WordPress because they are afraid of losing their changes. Hence WordPress websites are never updated de facto.

## How to get rid of WordPress?

Let's imagine we could use WordPress and WooCommerce for what they worth only which are a blog system and an online store system. 
The first thing we want to do is to remove the risks that are the plugins, and only install WooCommerce inside WordPress. 
The second thing we want to do is to get rid of the themes too. That's when we start looking at Headless WordPress and find out about the WordPress API and WooCommerce API. 

### WordPress API

WordPress, since its version `4.7.0` (released in December 2016), offers a RESTful API  that is to say 13 years after its first release in 2003 and only 3 years ago from the time of the writing of this article. 

The API allows interactions with WordPress using JSON (JavaScript Object Notation) format only. While for requesting data from it, it does not require authentication if you wish to edit, create, or delete information you will need to authenticate. It is worth noting that WordPress only supports Cookie Authentication natively, but some plugins allow for more types. 

The root endpoint is http://yoursite.com/wp-json/. From there you will be able to see all the available endpoints. 
But let's dig into some examples:

- To retrieve the list of posts (articles) on your blog you run a GET request at the endpoint http://yoursite.com/wp-json/wp/v2/posts/ you will then receive the first page of the posts in JSON format. 
Example of result:
```shell
$ curl -X GET http://yoursite.com/wp-json/wp/v2/posts/
[
	{
		"id": 6214,
		"date": "2019-07-18T01:00:21",
		"date_gmt": "2019-07-18T01:00:21",
		"modified": "2019-07-18T03:23:13",
		"modified_gmt": "2019-07-18T03:23:13",
		"slug": "sluggish-slug",
		"status": "publish",
		"type": "post",
		"title": {
			"rendered": "The website is open!"
		},
		"content": {
			"rendered": "content",
			"protected": false
		},
		"excerpt": {
			"rendered": "excerpt",
			"protected": false
		},
		"author": 38,
		"featured_media": "src",
		"comment_status": "open",
		"ping_status": "open",
		"sticky": false,
		"template": "",
		"format": "standard",
		"meta": [ ],
		"categories": [
			2
		],
		"tags": [
			6,
			24
		]
	}
]
```

- To retrieve a media that was used in a post you run a GET request against the endpoint http://yoursite.com/wp-json/wp/v2/media/`<id>`, replace `<id>` by the actual id of the media, then the source_url in the object response attribute will lead you to the actual media. 
Example of result:
```shell
$ curl -X GET http://yoursite.com/wp-json/wp/v2/media/335
[
	{
		"id": 335,
		"date": "2019-05-08T10:53:15",
		"date_gmt": "2019-05-08T10:53:15",
		"guid": {
			"rendered": ""
		},
		"modified": "2019-05-08T10:53:15",
		"modified_gmt": "2019-05-08T10:53:15",
		"slug": "thumbnail-mmfmydygxdc-7",
		"status": "inherit",
		"type": "attachment",
		"link": "http://yoursite.com/thumbnail-mmfmydygxdc-7/",
		"title": {
			"rendered": "thumbnail-MmfmyDygxdc-7"
		},
		"author": 31,
		"comment_status": "open",
		"ping_status": "closed",
		"template": "",
		"meta": [ ],
		"description": {
			"rendered": "<p class=\"attachment\"><a href=''><img width=\"300\" height=\"169\" src=\"\" class=\"attachment-medium size-medium\" alt=\"\" srcset=\"300w, 768w, 1024w, 1568w, 450w\" sizes=\"(max-width: 34.9rem) calc(100vw - 2rem), (max-width: 53rem) calc(8 * (100vw / 12)), (min-width: 53rem) calc(6 * (100vw / 12)), 100vw\" /></a></p>"
		},
		"caption": {
			"rendered": ""
		},
		"alt_text": "",
		"media_type": "image",
		"mime_type": "image/jpeg",
		"media_details": {
			"width": 1919,
			"height": 1078,
			"file": "2019/05/thumbnail-MmfhyDygxdc-7.jpg",
			"sizes": {
			"thumbnail": {
				"file": "thumbnail-MmfmyDygxdc-7-150x150.jpg",
				"width": 150,
				"height": 150,
				"mime_type": "image/jpeg",
				"source_url": ""
			},
			// ...
		},
		"image_meta": {
				"aperture": "0",
				"credit": "",
				"camera": "",
				"caption": "",
				"created_timestamp": "0",
				"copyright": "",
				"focal_length": "0",
				"iso": "0",
				"shutter_speed": "0",
				"title": "",
				"orientation": "1",
				"keywords": [ ]
			}
		},
		"post": null,
		"source_url": "",
		"_links": {
			"self": [
				{
					"href": "http://yoursite.com/wp-json/wp/v2/media/335"
				}
			],
			// ...
		}
	}
]
```

So you can see by yourself consumption of the API is pretty straight-forward and allows you to retrieve any data pretty easily. 

For more details, the official documentation for the WordPress REST API is available at that address: [https://developer.wordpress.org/rest-api/](https://developer.wordpress.org/rest-api/){:target="_blank"}

### WooCommerce API

WooCoomerce has been offering a RESTful API to its users for a longer time than WordPress. The first WooCommerce API was released with WooCommerce `2.1.0` in February 2014 which is almost three years before WordPress' REST API.

Pretty commonly used, for example when you set up your logistics with ShipBob they will use the API to retrieve your shop orders automatically. 

It is important to note that the original WooCommerce API after several updates has been deprecated and relabeled Legacy API. And because of the release of the WordPress API, WooCommerce decided to fully rework their API to extend the WordPress API directly. 

Our recommendation here is to use the latest version which is at the time of this article is WooCommerce API v3. Not the Legacy one but the current one.  

When using the API whether the Legacy or the current one, you need to create first an API token in the settings of WooCommerce steps to follow are described here: [https://docs.woocommerce.com/document/woocommerce-rest-api/](https://docs.woocommerce.com/document/woocommerce-rest-api/){:target="_blank"}

If you want to use then the API in your code check out how to use the authenticate with the token here: [https://woocommerce.github.io/woocommerce-rest-api-docs/#authentication](https://woocommerce.github.io/woocommerce-rest-api-docs/#authentication){:target="_blank"}

Now let's dig into some examples: 
- To create an order you run a POST request against that endpoint http://yoursite.com/wp-json/wc/v3/orders with a JSON object describing your order. Complete example details available here: [https://woocommerce.github.io/woocommerce-rest-api-docs/#create-an-order](https://woocommerce.github.io/woocommerce-rest-api-docs/#create-an-order){:target="_blank"}
- To retrieve the list of products on sale you can run a GET request against that endpoint http://yoursite.com/wp-json/wc/v3/products. Complete example details available here: [https://woocommerce.github.io/woocommerce-rest-api-docs/#list-all-products](https://woocommerce.github.io/woocommerce-rest-api-docs/#list-all-products){:target="_blank"}

For more details, the official documentation for the WooCommerce REST API is available at that address: [https://woocommerce.github.io/woocommerce-rest-api-docs/#introduction](https://woocommerce.github.io/woocommerce-rest-api-docs/#introduction){:target="_blank"}

### Modern JS Front-end App

If you are a web developer, you are probably using one of these modern JS frameworks to develop modern websites. 

- [Angular](https://angular.io/){:target="_blank"}
- [React](https://reactjs.org/){:target="_blank"}
- [Vue.js](https://vuejs.org/){:target="_blank"}
- ...

What is different with these from tech like PHP or Ruby on Rails, it is that the back-end and server logic is decoupled from them. 
Hence using these frameworks we generally go for an architecture of a decoupled front-end that consumes web services. Note that this also allows front-ends to work offline. 

### Let's combine both!

Simply now use your favorite HTTP Client to simply consume the WordPress and WooCommerce API

We suggest,
- For React and Vue to use: [https://github.com/axios/axios](https://github.com/axios/axios){:target="_blank"}
- For Angular to use: [https://angular.io/guide/http](https://angular.io/guide/http){:target="_blank"}

### The middleware for the extra security

To keep our WordPress away from curious eyes, we decided to hide its usage from the front-end and to do that we decided to develop a middleware that would interface our Angular front-end with the WordPress backend. 

Below is the architecture we went with:

![Muted Wordpress](/assets/posts/muted-wordpress/architecture_wordpress_muted.svg)

- Front-end running on Angular and Typescript
- Middleware running on Node.js and Typescript
- Back-end running on WordPress
- CDN and storage are respectively running on AWS CloudFront and AWS S3.

Note that to automate the upload of the media to S3 in WordPress we installed the plugin [WP Offload Media Lite](https://wordpress.org/plugins/amazon-s3-and-cloudfront/){:target="_blank"}.

Making the total count of our plugins installed into WordPress to only 2: _WooCommerce_ and _WP Offload Media Lite_ that we feel safe to update at any time.

Thus simply turning WordPress into a backend system, when we want:

- To post an article, we simply add a post in WordPress,
- To host a picture, we simply upload it into WordPress media, and retrieve the CDN link,
- To do some changes in some parts of our website, we edit a WordPress page that is used to load content on our website,
- To add a product, we simply add it into WooCommerce,
- ...

## Difficulties Encountered

- The WordPress API is actually slow: 
[https://stackoverflow.com/questions/45421976/wordpress-rest-api-slow-response-time/45425091#45425091](https://stackoverflow.com/questions/45421976/wordpress-rest-api-slow-response-time/45425091#45425091){:target="_blank"}
Though a plugin seems to help for that, by caching answers from the API:
[https://wordpress.org/plugins/wp-rest-cache/](https://wordpress.org/plugins/wp-rest-cache/){:target="_blank"} (We haven't tested it yet).

- Under special circumstances, you may want to register custom endpoint 
[https://developer.wordpress.org/rest-api/extending-the-rest-api/adding-custom-endpoints/](https://developer.wordpress.org/rest-api/extending-the-rest-api/adding-custom-endpoints/){:target="_blank"}

- To keep WordPress fully hidden behind our middleware, we had to filter all the links returned by WordPress to make sure they either use the CDN, use a vetted domain, or simply don't appear in the API calls answers. For that, the plugin _WP Offload Media Lite_ helps a lot for the media, but for example with internal links to products or posts, we apply filters on the JSON answers from WordPress in our middleware.


## Final Thoughts

For us at Pixelmatic, to be able to fully customize the front-end as we want, while also keeping our website more secure is a major win for us. Admittedly the infrastructure needs are bigger but the maintainability and stability in the long term are higher. 