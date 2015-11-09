---
id: 300
title: DNS names as mobile phone numbers
author: argp
layout: post
guid: http://argp.gr/blog/?p=300
permalink: /2006/02/22/dns-mobile-phone-numbers/
aktt_notify_twitter:
  - no
categories:
  - research
  - security
tags:
  - dns
  - petname
  - research
  - security
---
A few hours ago I found an [article][1] on [IBM developerWorks][2] proposing the use of DNS names on mobile phone networks with the goal of allowing end users to dial a name instead of a number.

The author does not go into any specific engineering details, but to make such a system scale you would need to introduce some sort of hierarchical DNS structure similar to the one used in the wired Internet. We should also keep in mind that alternative access methods for mobile phone networks, such as 802.11, are quickly becoming widely deployed.

All these make it clear, at least to me, that a DNS infrastructure for mobile phone networks is not a good idea; in my opinion it would create many more problems than it would solve. As is the case on the Internet, DNS creates huge security problems like DNS spoofing, cache poisoning, phishing, and others. Introducing the same problems in mobile phone networks does not sound promising without having some very clear advantages.

No one is really typing numbers anyway. We just select them from a phone number list that operates more or less as a [petname system][3]. When you want to call someone you look through your list for the petname you have assigned to them. When an incoming call arrives the phone displays the petname you have assigned to the person calling you. In both cases the software of the phone locally makes the translation between a user-defined name and a mobile phone number, which guarantees a certain level of authenticity.

 [1]: http://www-128.ibm.com/developerworks/wireless/library/wi-domain/?ca=dgr-lnxw06DNS4Cells
 [2]: http://www.ibm.com/developerworks/
 [3]: http://www.erights.org/elib/capability/pnml.html