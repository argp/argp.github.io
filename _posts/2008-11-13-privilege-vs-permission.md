---
id: 84
title: privilege vs. permission
author: argp
layout: post
guid: http://argp.gr/blog/?p=84
permalink: /2008/11/13/privilege-vs-permission/
aktt_notify_twitter:
  - no
categories:
  - research
  - security
tags:
  - acl
  - authentication
  - authorization
  - permission
  - privilege
  - trust management
  - æther
---
The majority of published papers and articles on the area of information security use the terms *privilege* and *permission* interchangeably. Even [Wikipedia&#8217;s entry on privilege][1] seems to follow this practice. However, one of the foundations of dynamic trust management is the clear distinction between an entity&#8217;s privileges and its permissions.

A privilege is an authority given to an entity that approves a specific operation on a specific resource. For example, an entry in an Access Control List (ACL) specifies a privilege, not a permission. A permission, on the other hand, is a value reached when an entity&#8217;s privileges, as well as other of its attributes, are evaluated. Therefore, the fact that an entity has been granted a privilege does not necessarily mean that it is able at a given time to perform the specified operation on the specified resource.

The dynamic trust management system [&aelig;ther][2] I have designed and implemented as part of my Ph.D. provides an example of using this distinction between privilege and permission in practice.

 [1]: http://en.wikipedia.org/wiki/Privilege_(computer_science)
 [2]: http://www.mee.tcd.ie/~ledoyle/EMERGINGNETWORKS/pages/aether.htm