---
layout: post
title:  "Get someone to look at your code!"
date:   2014-10-15 15:00:37
categories: programming side-project 
---


Ten months ago, I agreed to build software for a driving school as a side project.
Today the project is 90% done, so only the [other 90%](https://en.wikipedia.org/wiki/Ninety-ninety_rule) remains.

I had been hacking away on the application for a couple of months before everything became too big to keep in my head.
In a moment of enlightenment, I decided to hire an experienced developer on odesk to take a look at my code. In less than 2 hours he was able to tell me my what my problem was (fat controllers, skinny models).
I now have better code reuse, less bugs and more testing and it only cost me $50 in developer fees.
Peanuts compared to the time I gained as a result.

I'm the only developer on this project, and I'm not even a programmer in my day job.
I choose to code the application in Ruby On Rails, as I had some familiarity with the framework.

I dove in: head first and learning on the way. As so many of us do.
My code gradually became better as I discovered functionality provided by Rails and the proper way to do certain things.
For a couple of months I hacked away, adding needed functionality.
Along the way, the application became bigger and it was getting harder to keep everything in my head at once. 
When I added or changed functionality, I now frequently broke other stuff.

Realizing my problem, I started looking into adding automated tests. 
Yes, you read it right. 
I hadn't done that before. I never realised I needed them.
After reading up on testing, I tried to write some meaningful tests for my application.
But I never really got it working, it was as if I could not wrap my head around the tests.
So I thought: I'll just get someone on odesk to write some for me.
That way, I'll be able to look at them and write new ones myself.

I hired an experienced dev and encouraged him to additionally tell me about coding errors I made.
The guy took one short look at my code and told me where I'd gone wrong: too much code in the controllers, not enough in the models.
I had difficulty accepting at first: I'd become pretty protective of my coding style.
But after looking at it for a bit, there was no denying: I'd replicated functionality accross my controllers.
Moving this in the models meant I could just use the method on the model itself, instead of writing the code each time.
I had not even realised I'd made this mistake!
In rectifying this, my controllers instantly became more readable, my application better testable and I removed bugs where I had forgotten to make the same changes accross the controllers.

Moral of the story: get other people to look at your code.
If you don't know anyone, pay someone to do it. 
What you loose in money, you'll gain in time!

