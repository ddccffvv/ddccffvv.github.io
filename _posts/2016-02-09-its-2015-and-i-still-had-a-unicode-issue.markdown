---
layout: post
title:  "It's 2016 and I still managed to have a unicode issue"
date:   2016-02-08 08:30:37
categories: summary
author_name : Stijn
author_url : author/stijn
author_avatar: stijn 
show_avatar : false
feature_image: feature-wolf
show_related_posts: false
square_related: recommend-wolf
---

If you ever run into an issue that looks related to unicode/utf (you get characters such as "\00eb"), check if it's installed on your system.

I recently was stumped by this, because my sinatra/ruby application worked on my dev machine, but not on the server (I've heard that one before! ;-) ).
Turns out utf wasn't installed on the server (a debian machine).

For future reference, it's easy to install:

1. append *en_US UTF-8* to /etc/locale.gen
2. run "locale-gen" as root
3. (optional) export this variable in your terminal *export LANG=en_US.UTF-8*
4. Make the environment variable available for apache/passenger/ruby. You do this by putting *SetEnv LANG en_US.UTF-8* in the appropriate vhost.
