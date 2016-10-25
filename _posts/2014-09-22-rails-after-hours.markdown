---
layout: post
title:  "Lesson from a side project"
date:   2014-09-22 15:00:37
categories: programming side-project 
author_name : Stijn
author_url : author/stijn
author_avatar: stijn 
show_avatar : false
feature_image: feature-wolf
show_related_posts: false
square_related: recommend-wolf
---


Ten months ago, I agreed to build software for a driving school as a side project.
Today the project is 90% done, so only the [other 90%](https://en.wikipedia.org/wiki/Ninety-ninety_rule) remains.
Below is one of the most important things I've learned.

### Clients don't know what they want, but they know what's wrong with what they get.
I found it very difficult to translate client requirements into code. 
While clients were able to talk me through the current working of a feature, conversation abruptly stopped when I started asking about the way they would like the feature to work in the future. A question such as "How would you like to schedule your lessons?" is just to broad to answer. 
I could try ask more specific questions, but there are so many details that only come up during implementation.
In the end, I believe it's up to the programmer to make his application a joy to use for the client.

After some experimentation, I settled for the following approach: 
We'd have in depth discussions about how some feature should work.
In addition to functional questions, I'd also ask a lot of questions with regards to usage: "How do you do *x* right now?", "How many times do you do this a day?", "Is that a lot of effort?", "What don't you like about how *y* currently works?"
I'd then use this knowledge and as much common sense as I could muster to implement a minimal feature.
I'd show them the new feature as soon as it was half-way working and ask them to use it while I was on the phone.
The simple act of interacting with the solution seemed to make it easy to give valuable feedback: "Well, *a* is ok but I can't do edge case *x*. And normally I do *a*, *b* and *c* in the same order but now I have to click a lot to do the same".

With this feedback, I was able to improve significantly on the original implementation, to great satisfaction of my client.
It seems to me that this method is pretty efficient maximising utility for the client while minimising implementation effort.

I'm settling on this method for now, but I'm interested to hear about your client communication in the comments!

