---
layout: post
title:  "Vim Cheatsheet (in progress)"
date:   2015-07-02 15:00:37
categories: vim
author_name : Stijn
author_url : author/stijn
author_avatar: stijn 
show_avatar : false
feature_image: feature-wolf
show_related_posts: false
square_related: recommend-wolf
---

My vim cheatsheet (an ongoing effort)...

##Actions inside blocks

    cit - change inside tag: delete text in between tags and enter insert mode
    cat - change inside tag (include tags): delete text in between tags and enter insert mode (tags included)
    dit - delete inside tag
    dat - delete inside tag and tags
    ca" - change text in between quotes
    da" - delete text in between quotes

## Searching 

    set smartcase "search case sensitive if at least one letter is uppercase, otherwise search case insensitive
    \c            "search case insensitive (let this appear anywhere in search string)
    \C            "search case sensitive (let this apprear anywhere in search string)

## Spell check

    :set spell spelllang=en_us
    :set nospell

