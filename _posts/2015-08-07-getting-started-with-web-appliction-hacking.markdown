---
layout: post
title:  "How to get started in offensive security"
date:   2015-09-02 15:00:37
categories: hacking web applications pentesting 
---




##Start with web application pentesting

The security field is vast and you can't become an expert in everything at once. Even better: most professionals specialize, why should you have to know everything? 

A good starting point is web application security: it's the default mode for new applications which means that there are enough of these that need security testing. Additionally, complex web applications are usually a beautiful mess of different technologies. That's always a good breeding ground for security vulnerabilities.



##What tools should I use?

Woah, hold your horses there young fella. 
Yes it's true: there are many excellent tools out there. But using them is like getting in the cockpit of an airplane without proper instruction: you'll never get the thing of the ground. And if by chance you do, how are you going to get it back on the ground?

No, you'll have to start by understanding the underlying principles. 
Vulnerabilities are the result of insufficient understanding of fundamental principles. So, your job is to understand the fundamentals better than the other guy.
The trick is that there's no trick: we all have to start at the beginning and gain our skills and experience through hard work.



##That sounds hard!

Well it is! And that's the point. 
If it were easy, there would be no confusion. And that confusion? That's where the security vulnerabilities lie..
But don't get discouraged now, it's not impossible either. You just have to be persistent, that's all.
Do you like finding out how things work? Good, that's enough. Once you know what makes something tick, you know how to break it.



##So where do I start?

Start with HTTP. Almost everything on the web runs on HTTP. You have to know how it works.
I won't send you to the RFC (just yet), but I predict you'll read it anyway sometime in your career.
Here is a good resource that will get you started: http://www.jmarshall.com/easy/http/
A good way to become familiar with HTTP (besides to reading the tutorial) is to use an intercepting proxy.
This is a tool that sits between the browser and the server. 
If you learn by doing (like I do), an intercepting allows you to see all the HTTP requests your browser makes on your behalf. 
It even lets you change them. Believe me: that's something you'll do a lot later on!
Most in the industry use Burp, so I suggest that's what you use. 
They have a free version that's more than enough for your use. Here's a nice introduction tutorial: http://resources.infosecinstitute.com/burpsuite-tutorial/
While you're getting familiar with HTTP, make sure you pick up on all that html and javascript stuff that's going on.
It'll come in handy in a bit.

Ah, and by the way, did you know that there's a big problem with HTTP, it's stateless... Can you tell me why that's a problem and how we're trying to fix it?



##The basics of vulnerabilities



Well, we're getting in deep now. When talking about web application security, you'll quickly hear the terms "sql injection" and "cross-site scripting" thrown around.
Yes it's true, these are pretty important. SQL-injection requires you to learn yet another technology, so we'll leave that for now. 

Cross-site scripting however, that's something you're ready for. Here's a nice tutorial: http://www.steve.org.uk/Security/XSS/Tutorial/


As an aside, have you noticed that it's difficult to test these things on somebody else's website? It would be handy to have your own setup, right? 
Well, that's a great idea! The best way to learn about web applications (and to learn what can go wrong) is to write one yourself.
Don't be intimitated, we have fantastic frameworks these days that will help you out. Besides, you'll have to learn basic programming anyways. 
How else are you going to learn how a programmer thinks? 
Most of the industry uses python, go with that. Flask is a simple python framework that's made for writing web applications. 
Additionally, it has a fantastic tutorial to get you started: http://flask.pocoo.org/docs/0.10/quickstart/

Back to sql injection. That's a big one. Many of the breaches you read about in the news are the result of sql injection.
You'll have to learn some SQL. That's the language we use to retrieve data from the database. It's pretty powerful, that's exactly what we'll use to our advantage!
To get started, it's a good idea to hook up a database to your web application. Here's how to do that: https://www.syncano.io/intro-flask-pt-2-creating-writing-databases/
Once you've done that, you understand enough to experiment with sql injection.
I like this tutorial: http://www.w3schools.com/sql/sql_injection.asp Can you replicate it in your Flask app?



## Where to go from here



There are many other things to talk about, but we've already covered a lot of ground here.

After you've completed everything in here, you're well on your way to becoming a pentester. Don't get discouraged if it takes a couple of weeks to work through the post, it's meant that way. Remember, nothing worth knowing comes easy. Just be persistent, you'll get through it!

If you're looking to go further, I suggest you get the "web application hacker's handbook". It's available on amazon and the bible for all things web application security related. Good luck!

