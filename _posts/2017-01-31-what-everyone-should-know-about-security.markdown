---
layout: post
title:  "What every developer should know about security"
date:   2017-01-31 08:30:37
categories: security 
author_name : Stijn
author_url : author/stijn
author_avatar: stijn 
show_avatar : false
feature_image: feature-design
show_related_posts: false
square_related: recommend-wolf
---

This advice covers 80% of what I learned in half a decade as a pentester. 
Use it to your advantage (or don't, that's up to you).

Note: this post is based on a ptacek comment on [ycombinator](http://news.ycombinator.com).
I can't find the comment anymore.
If you do, please let me know.

## Know what you are building

This seems quite obvious, but I found it one of the biggest indicators of security: if the developers know the business domain and their tools, the hackers will be up against quite a challenge.
In my opinion, "quality" is directly tied to security.

## Prepare for disaster

It's pretty hard to be flawless all the time.
Related to the security domain: all your systems should be fully patched all the time, your code should not contain any bugs, your users should not give away their passwords,...
You get the message. 

It's better to realise something will go wrong and have a good backup & restore plan:
Plan to update (or rebuild) your platform software at inconvenient times. Document and dry-run your update process, so you know it will work on no notice.

This became a lot easier recently, now that we have configuration managers and cloud providers. Use these, but make sure you have a plan for when the secrets to access your provider get stolen!

## Make sure to keep an eye on 3rd party components

Using libraries with known security issues is an open invitation to get hacked.
Put someone on your team in charge of tracking your dependencies and have a process by which you periodically check to make sure you're capturing upstream security fixes.
There are some tools that can help you with this, here are two examples:

1. [App Canary](https://appcanary.com/)
2. [SourceClear](https://www.sourceclear.com/)

## Use standard cryptographic options

Use TLS to encrypt data in motion and use GPG to encrypt data at rest, and don't do any other kind of crypto.
Don't try to invent your own encryption scheme (unless you're an expert in the field).

## Keep your code boring

Stay on your platform's "golden path" for web security issues (meaning: use the functionality provided by the framework).

## Watch out for these known difficult patterns:

The following pieces of functionality get a lot of attention from attackers and rightfully so.
They have proven themselves very difficult to implement correctly. 
Make sure to pay a lot of attention to the following:

1. Triple check any piece of code that "shells out" to command line tools.
2. Be wary of library code for web apps that includes "native" C/C++ code.
3. Triple-check code that handles direct file uploads and downloads. The file system introduces a new namespace, so upload/download code needs to juggle different privilege and authorization domains to handle it.

## Pay attention to the trust boundaries

Trust boundaries are areas where users suddenly are granted more rights (for example: the login mechanism).
By their nature, these are interesting to attackers. 
In the same vein as the advice in the previous point, make sure you pay a lot of attention to how they are implemented.

By the way, it's a good idea to do administration out-of-band. Write a separate admin app (bonus: the admin app can look bad, and so is less expensive to maintain) that requires a VPN connection to access. Avoid special-privilege accounts in your normal apps.

## Be open to security researchers

Have a security page. Have that page very cordially invite people to submit security flaws to an email address at your site; provide a PGP key for it. If you don't have this page, you should know that you are inviting people to report security flaws to Twitter.


