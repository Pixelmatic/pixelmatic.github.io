---
layout: post
title:  "A password generator to save your life"
excerpt: "Living in modern society, most of the users of online services have to bear the pain to remember the access to plenty of platforms including websites, services, apps, bank account, email, etc. The login credentials cannot be too simple for security reasons, or too complex to remember it clearly. I believe everyone could lose some of the credentials or cannot recall it clearly."
author: Stefan Liu
categories: Tools
tags: [ tools, cyber security, password, credentials ]
---

*Original article from [https://blog.devfans.io](https://blog.devfans.io/a-password-generator-to-save-your-life/){:target="_blank"}*

Living in modern society, most of the users of online services have to bear the pain to remember the access to plenty of platforms including websites, services, apps, bank account, email, etc. The login credentials cannot be too simple for security reasons, or too complex to remember it clearly. I believe everyone could lose some of the credentials or cannot recall it clearly if he’s keeping more than five quite different access passphrases. And if you are trying to use similar passwords for multiple services, you are possible to mess up with them easily and using similar passwords is not a good practice for security reasons, since you even don’t know it if some services you ever used are hacked and your credentials are posted to public pages someday.

#### Is there a perfect solution for this?

As far as I know, not yet. But, some small security utilities can probably ease the pain to remember all the credentials and reduce the risk of access leaking. The one I am gonna introduce in this post is [PassWizard](https://passwizard.github.io){:target="_blank"}, a small static page I wrote to serve as a password generator.

#### How does a password generator save your life

The idea behind **PassWizard** is quite simple indeed. You feed in a simple passphrase to it and specify which account on which platform, then it will generate the repeatable random password table for you to select. It has some features that matter for your concern:

+ *Repeatable*. Yes, if it can not repeat the password table with the same input, then every user of it is fucked up.

+ *Static and No-Tracking*. It’s a static web page hosted on GitHub which mainly a canvas operated by js code on the page, and it does not make any communication to anything else for the password generating process. You don’t need to worry about your credentials are stored somewhere and might be leaked someday. No one is tracking the service and I wrapped the input interface into a canvas on the page which means it has a bit less risk of leaking if your computer or browser is hacked or listened by some methods.

+ *Randomness*. It has to be random and less related to some common patterns. The website implements some tricks to reach that, so a single character change in the input would cause an absolute different password table generated.

+ *Complexity*. With randomness, it's possible the password generated could be quite simple in chances, that would not be something we expect, so there're other tricks in the implementation to get rid of it. Maybe the algorithm is not perfect yet, but it's working well. Also, the input fields support every kind of characters you can type with your keyboard. If it's not, well I need to figure it out with your feedback then.

#### Using [passwizard.github.io](https://passwizard.github.io){:target="_blank"}

Here to explain the interface of PassWizard (Navigation: `enter` and `mouse cursor`):

![Passwizard](/assets/posts/password-generator/a-password-generator-to-save-your-life-0.png)

+ Go to the site and it’ll show two blank input fields. The first one is the passphrase you want to use, it could be a sentence or anything you can get from your mind. Press `enter` key to go to the next input, and the first field would be automatically hidden if not focused or hovered.

+ The second input field is for the account. It could be the username or an email address, or anything for there’s no limitation. But the intention is for you to specify your user account identity. Press `enter` to jump to the next page.

+ On the next page, you can specify the platform or service name in the input field, and yes without any limitation. You may notice every time you change a character, the password table below will be changed totally.

+ Click any type of the password in the table to select the one you want to use. It’s copyable. You can use them now.

+ You need to remember the passphrase (The first input) and which password type you choose which each platform. This way, you can keep a single private passphrase and use it for every account on every platform with knowing which type of password you chose for each platform. And, yes you need to mark the passphrase into your mind clearly, and that’s the single thing you truly need to take care of.

#### Using PassWizard Wechat mini-program

![PasswizardMiniProgram](/assets/posts/password-generator/wechat.mini.png)

Scan below QR to try it:
![PasswizardQR](/assets/posts/password-generator/passwizard.qr.png)


#### NOTES

+ Please access PassWizard at: [https://passwizard.github.io](https://passwizard.github.io){:target="_blank"} and its source code is hosted at [https://github.com/passwizard/passwizard.github.io](https://github.com/passwizard/passwizard.github.io){:target="_blank"}.

+ If you are interested in optimizing the implementation of it or polishing it with brilliant new ideas, let me know.
