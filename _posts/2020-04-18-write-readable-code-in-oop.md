---
layout: post
title:  "Write readable code in OOP"
excerpt: "In this article, John shares to you his thoughts and the different approaches to write readable code that can outlive the time."
categories: Articles
author: John Yu
tags: [ articles, oop, code quality, qa ]
---

## Inspired by reading

People read books, read various types of books, for different purposes. The responsibility of books is to deliver information. Otherwise, they're just paper.  

This kind of information delivery is special, it crosses space and time, authors hundred years ago talk to their reader through their books.  

A piece of code is an article, a project is a book. The book's reader contains not only our human-beings but also machines, the computer. It deliveries information from human to machine. 
​
### In terms of reading the book
​
The book contains instructions on how to do specific jobs that you asked a computer to do. Computers hate ambiguity, everything that requires a computer to read needs to be accurate.  

If your book, or say code, is being accepted by the compiler and is compiling, congratulations you successfully eliminated ambiguity. 
​
## Ambiguity
​
Remember not only a computer is the reader, humans as well, developers. Luckily we human-being allows the certain degrees of ambiguity, we read documentation composed by the code writer, we directly contact the writer to ask questions, no problem.  

However, this is also where most of the problems - buggy code, unreadable code - we get came from. The ambiguity.  

Information is lost when:  
* There are magic numbers in the code
* Bad named variable/method/class without comment
* Find everything you need by following threads in a large bowl of noodles
* Repeating code with slightly different lines of code
* The author doesn't care
* The author resigned
* No documentation
* Documentation out-dated  

Believe me that if you fetch a random coding tip, or just looking at a feature of a programming language, there is always a smell of eliminating the ambiguity there. 
​
## Speak the same language

We know that for the same thing, the more we do it, the easier we can do. Remember the process of how you acquire your secondary language, how you make your habit of running every day. How difficult you read news written by your secondary language, by keeping looking up the dictionary. That applies to programming as well.  

I'm not talking about using the same programing language. But the same style of writing code, aka speaks the same language.  

If you are working in a team, you pretty much had been asked to follow a programming convention. That is literally to ask you to speak the same language in the team so that you can instantly understand what you're reading, and free your mind from "looking up the dictionary". It is worth spending a little time getting familiar with the convention so that you save a lot of time on looking up the dictionary, to make sure you have enough mind power to eliminate ambiguity - that's not an easy job.  

Furthermore, you might want to get familiar with every pattern of programming. They're pre-packed solutions that fit in a certain situation. If someone else uses one of these, you will instantly know the purpose of the entire piece of code by looking at the first few lines. That saves you time. It would be the same to you if you solve your problem by using some pattern, the other benefits too.  

UML is a kind of language that specifically define the problem and solution clear. Maybe not all the developers use that but what we can learn is, at least when people arguing each other and it turns out their understanding of the concept they are discussing is different, it could be better to use a more accurate language to describe your thoughts. 
​
## Get familiar with the business

You write code for a purpose. It doesn't make sense you're writing something that you don't understand. You will have many ways to archive your final goal, you need to use your knowledge to choose the most proper one. Programming a rocket is one thing while programming a toy rocket is the other thing. A real rocket requires one-time success while the toy one doesn't, you can crash your toy thousands of time for fun and no need to worry that will kill someone.  

Basically for every way you write code spend different time in the short term and long term. A carefully designed program saves time in the long term but will spend more in the short term. So choose wisely with your knowledge base on the purpose.  

Sometimes you will realize that the code is hard to read not because of ambiguity, but you're not familiar with the business. So if you're working on a simulator of Rally car game, make sure you understand how the car works, the rule of Rally race, and relative physics before getting your hand dirty. 
​
## Quality Quality Quality

Quality is not an optional item in the checklist, but something necessary. However quality has its cost, and quality has certain levels. We need to balance, make sure the quality reaches the most proper level at certain development stages.  

The same rocket example: we don't want to spend years of the time & money of a real rocket on a toy rocket. It is ok for a plastic rocket to fail and crash in the garden, trial and error just works. But it does not mean you don't need quality at all. At least need to make sure that your plastic rocket can do its job: fly and make people happy, and maybe you can play it multiple times.  

The other example: when the next step of your program is not clear, but you sure that something will happen. Make sure the remaining part of the program that less likely to be changed is capable to handle the varieties. 
​
## Common Practices
​
I assume no one wants to deal with noodle code. You will have endless bugs to fix, deadline delayed again and again. As soon as we know where we don't want to go, we just need to figure out what to do.  

You must hear about the terms like SOLID, Design Patterns, Decoupling, Refactoring, Smells of code, etc. What are they suggesting?  

Well, in my opinion, most of the practices share the same core of principle: don't repeat yourself(DRY). If you're dealing with two pieces of code that seem to be the same, or two classes/modules share the same responsibility - one of the common bad smells of the code.  

I want to extend the concept of DRY, that sounds like don't copy paste your code. Instead, you should have a feeling that something is wrong for example:
- Every time you feel that you're doing something you've already done, you're implementing a module that seemingly already partially implemented by the other module
- You are fixing a module again and again and it keeps producing more issues
​
You will either use the tool of *refactoring* to clean things up, or uses one of the patterns from your toolbox to handle the mess nicely.  

I will provide a resource list where you can check through that can help you to write readable code. However one take away is that none of these practices is the silver bullet. Use the proper tool, even modify the tool to solve your problem. Know the programming language you're working on very well, you will have a lot of problems to solve so don't waste time looking up the dictionary.  

Here's a resource list that can help you on different stages:  

- The basic principle: [SOLID](https://en.wikipedia.org/wiki/SOLID)  
- Check how far you need to go before commit your code: [*Code Complete by Steve McConnell*](https://en.wikipedia.org/wiki/Code_Complete)  
- Give you the sensitivity of potential problematic code, and tools to fix them: [*Refactoring Improving the Design of Existing Code by Martin Fowler*](https://martinfowler.com/books/refactoring.html)  
- Here's a handy website in case you don't have access to the books above: [*Source Making*](https://sourcemaking.com/refactoring/smells) (It also includes some more useful information that helps you with writing readable code.)

## Tools

You can decide which piece of code that should be refactored according to your experience. But there are tools like static analysis tools available to analyze your project to find out the potential issues. Here is a static analysis tool of C#: [Link](https://stackoverflow.com/questions/38635/what-static-analysis-tools-are-available-for-c)  

Of course, it is possible that you can finish all your work do all the refactoring with notepad. But a powerful toolbox can save much of your time, even it  will cost you some money, I prefer JetBrains' product.
