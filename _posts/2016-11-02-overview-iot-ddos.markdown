---
layout: post
title:  "Overview of the recent DDoS Attacks (September/October 2016)"
date:   2016-11-01 08:30:37
categories: random 
author_name : Stijn
author_url : author/stijn
author_avatar: stijn 
show_avatar : false
feature_image: feature-paper
show_related_posts: false
square_related: recommend-wolf
---

##The Problem

With the spreading prevalence of embedded devices online (the "internet of things"), DDoS organisations discovered a new source of bots. 
Anti-DDoS providers are not prepared for the sudden enormous surge in data/bandwidth that can be directed towards their clients.
In other words: at the moment, the offense is better than the defense.

##High profile cases

* 11/9: Krebs on security site was put offline by a DDoS attack twice the size of the biggest attack the anti-DDoS provider had ever seen (600+ GB/s).
Traffic was a mix of  SYN, GET, POST floods + a substantial % of traffic was spoofed GRE traffic (= unusual).

* 23/9: OVH was the target of a DDoS attack. 1000GB/s!!
Traffic: unknown, probably identical as the Krebs attack.

* 21/10: DynDNS was the target of a DDoS attack. DynDNS is the DNS provider for multiple sites. When it went down, its clients also were unreachable: reddit, twitter, paypal,...
Traffic: targeting the Authorative DNS infrastructure (DNS requests to random subdomains)

As I understand it, the primary impact of this kind of attacks is on the available bandwidth of the provider.
With such large volumes reported, this becomes the first problem (as real clients cannot get to the resource due to congestion of the pipe). 
Of secondary importance is overwhelming of the service itself (application-level DDoS). 
When the upstream provider becomes able to filter out enough traffic, the attacks can change to target the application itself.
The bots are abundant enough to exhaust application resources, which will have the same effect from the end-user point of view.

##Characteristics of the botnet

The botnet is likely controlled by "Mirai", software written to command and control mostly embedded devices. 
The source code of this software was leaked on the internet in September and contains functionality for the standard attacks described above.
At the time of writing, there are around 200k effected devices online (1.5 million affected devices in total), according to this [tracker](https://intel.malwaretech.com/botnet/mirai/?h=24).
The botnet is comprised of: 96% IOT (almost all IP cameras made by a Chinese vendor), 4% home routers, less than 1% compromised Linux hosts

##Mitigation
Providers are currently scrambling to add more capacity to their offerings.

On top of that, existing publications designed to limit spoofed IP traffic (a big enabler for most of these attacks) are being reconsidered. 
Top options are trying to filter ingress traffic ([BCP38](http://www.bcp38.info/index.php/Main_Page)) and source address validation ([SAVE](https://lasr.cs.ucla.edu/adas/)).
Implementing one of these would be a huge effort, requiring collaboration from a lot of actors on the internet and it remains to be seen how effective this countermeasures would be. (See [here](http://dyn.com/blog/recent-iot-based-attacks-what-is-the-impact-on-managed-dns-operators/) for a counter example).
In the case of attacks targeting DNS infrastructure, a promising option is [response-rate limiting](https://kb.isc.org/article/AA-01000/0/A-Quick-Introduction-to-Response-Rate-Limiting.html). 
This mitigation allows a DNS server to drop requests when it sees a sudden surge in requests to a certain resource (with only very small variations).
Implementing this countermeasure would limit the impact on the attack that brought DynDNS to its knees.

Taking down the bots (or preventing the control servers to take control) is also a massive undertaking.
Embedded devices have a historically bad record on security (often shipping with known holes) and patching (it's extremely difficult to remove the holes once the devices are in the open).
Still, improving the security of these devices is the best long-term solution and will require effort from all of us in the next decade.

Currently, your best bet is to have an anti-ddos provider and be in close contact with them. The best ones on the market are: [Akamai](https://www.akamai.com/us/en/resources/protect-against-ddos-attacks.jsp), [CloudFlare](https://www.cloudflare.com/ddos/) or [Incapsula](https://www.incapsula.com/ddos/). Additionally, make sure you drop all unwanted traffic as early as possible (at provider if possible, at your network edge,...)



