---
layout: post
title:  "Integrating security and DevOps"
date:   2015-08-05 15:00:37
categories: devops security
author_name : Stijn
author_url : author/stijn
author_avatar: stijn 
show_avatar : false
feature_image: feature-wolf
show_related_posts: false
square_related: recommend-wolf
---

Lately, I've been fascinated by the DevOps movement.
This relatively new movement has a number of concepts at its core that us security folks could (ab)use.
'Automated testing', 'infrastructure-as-code' and 'continuous integration or delivery' help teams rapidly introduce new functionality by quickly detecting bugs and providing a clearly defined, automated and scalable infrastructure environment. 

The same concepts are interesting from a security point-of-view. 
If we are able to tap into automated tests or infrastructure as code, we would be able to provide timely and precise feedback on the security of a certain application or system.
Too often now, we schedule our scans or perform our pentests and come up with a report weeks or months later.
At a time when everybody else is working hard to bring down time-to-market, it is unacceptable to delay releases merely because security can't keep up.

> At a time when everybody else is working hard to bring down time-to-market, it is unacceptable to delay releases merely because security can't keep up.

I see at least two opportunities for security to be involved in the process: 1) use the infrastructure description to detect old or insecure packages and libraries and 2) introduce security tests in the test suite.

## Infrastructure as code

Modern projects often keep a list of all dependencies in a file. Examples are the ``Dockerfile`` (Docker), ``Vagrantfile`` (Vagrant) or a ``Gemfile`` (Ruby-on-Rails).
I've included an extract of an example Gemfile. This clearly shows the libraries and versions in use. [^1]

{% gist ddccffvv/25a66212b2fa6fe3602f %}

We can keep an eye on this list and automatically verify if there are known vulnerabilities for the libraries used in our organisation.
Of course, the hard part here is not scanning the list, but finding a well-maintained and up-to-date vulnerability database we can automatically search through.

> Use dependency lists to determine which libraries to track and provide specific feedback to each development team.

Various different communities are making efforts. These are some of the most complete-looking services:

* [Hakiri](https://hakiri.io/) (Rails) Keeps your project gems under constant supervision and will notify you when the next CVE vulnerability hits.
* [VersionEye](https://www.versioneye.com/) (PHP) Notifies you if one of your libraries became vulnerable. The service is also able to notify you when a new version of a library came out for different languages.
* [Gemnasium](https://gemnasium.com/) (Various languages) Similar to VersionEye, this service will alert you when new versions of libaries become available. No mention of any security checks though.

As it stands now, it is very likely that we'll have to keep on monitoring different security lists. 
The dependency lists though are a valuable resource: they provide us with a specific list of all libraries and versions in use in our organisation. 
We can use this to determine which libraries we need to track and allow us to provide specific feedback to each development team.


## Automated testing

Many development shops now run various tests as often as possible. 
A strategy used often is to run a reduced number of tests (keeping the runtime of these tests low) before accepting new code from a developer in the system.
Periodically (for example: nightly) they run an extensive test suite against the latest build system. 
Timing and number of different 'testing tiers' differ, but this is the general principle.
The rationale behind running various tests early and often is to detect potential issues as soon as possible. 
The faster and more accurate you can pinpoint a potential flaw, the easier and cheaper it is to fix. 
It really is a powerful system.

> The faster and more accurate you can pinpoint a potential flaw, the easier and cheaper it is to fix.

We, the security stakeholders, should really take advantage of these automated tests: We should help our developers to add security related tests to the suite.
In a first step, we might try to bring our existing tools: different scanners and fuzzers. 
That's a good first step and will help us detect low-hanging fruit early. 
There's a caveat here: one false positive blocking the developers from shipping some feature and they will be ready to cut you out. 
Be careful!

> Nobody wants to be the one who introduced a security issue in the payment calculation that allowed hackers to order goods for free.
> Let's help our developers avoid that scenario. 

The people developing new functionality and writing automated tests don’t often have a background or interest in security. 
As a result, they only test if business critical flows can be completed correctly (the so-called “happy path”). 
As security professionals, we know that security issues are the result of doing unexpected things and are – by definition – not on the happy path.
I think this is a great opportunity to help developers and testers put 'misuse-case tests' in the suite.
Of course, it is impossible to check for everything that can go wrong.
But we can at least try to detect some obvious issues early.
Nobody wants to be the one who introduced a security issue in the payment calculation that allowed hackers to order goods for free.
Let's help our developers avoid that scenario. 
I'm sure you can think of malicious scenarios that apply to your particular business.
Things that have gone wrong in the past are a good starting point.



[^1] Actually, the Gemfile doesn't have all the versions because you can choose to not specify a version. In that case, the package manager will install the latest version. The ``Gemfile.lock'' contains the exact versions of all libaries in use.
