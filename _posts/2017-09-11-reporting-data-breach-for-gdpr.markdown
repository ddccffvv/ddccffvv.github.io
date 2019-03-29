---
layout: post
title:  "Reporting data breaches: GDPR requirements"
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

This is what's required from a data breach notification point-of-view:

1. As the processor: you just have to inform your controller (so client in your case) "without undue delay" (so relatively quick). You only have to do this once you've come aware of a "personal data breach" (meaning, personal data is involved). You never directly communicate to the "data subject" (the person who's data was lost), it's the controller who has to do that.

2. As the controller: This one has been mentioned more often. You have to:
    * Report to the data protection authority (DPA) within 72 hours of becoming aware of the data breach, unless it's unlikely to result in a risk to the "rights and freedoms of natural persons". (this means, do report if there's a chance. if you don't report it, make sure to document why extremely well). The DPA for us is the privacy commission. Leaks can be reported here: https://www.privacycommission.be/fr/la-notification-de-fuites-de-donn%C3%A9es. 
    * To the "data subject" (person who's data was lost) if the breach is likely to result in a "high risk to the rights and freedoms of a natural person", you need to report "without undue delay" and in an easy to understand language. There's a loophole here: you don't have to report anything if you take "subsequent measures which ensure that the risk is no longer likely to materialise". (meaning: if you implement extra security measures, you don't have to report to the subject). However, be aware that the DPA might force you to report a data breach.
