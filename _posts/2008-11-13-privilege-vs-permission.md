---
title: Privilege vs. permission
layout: post
tags:
  - research
  - security
  - acl
  - authentication
  - authorization
  - permission
  - privilege
  - trust management
  - æther
---
The majority of published papers and articles on the area of information security
use the terms *privilege* and *permission* interchangeably. Even [Wikipedia's entry
on privilege](http://en.wikipedia.org/wiki/Privilege_(computer_science)) seems to
follow this practice. However, one of the foundations of dynamic trust management
is the clear distinction between an entity's privileges and its permissions.

A privilege is an authority given to an entity that approves a specific operation
on a specific resource. For example, an entry in an Access Control List (ACL)
specifies a privilege, not a permission. A permission, on the other hand, is a value
reached when an entity's privileges, as well as other of its attributes, are evaluated.
Therefore, the fact that an entity has been granted a privilege does not necessarily
mean that it is able at a given time to perform the specified operation on the
specified resource.

The dynamic trust management system
[&AElig;THER](http://www.mee.tcd.ie/~ledoyle/EMERGINGNETWORKS/pages/aether.htm) I
have designed and implemented as part of my PhD provides an example of using this
distinction between privilege and permission in practice.
