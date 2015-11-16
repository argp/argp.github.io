---
title: Why I don't like network-layer security systems
layout: post
tags:
  - research
  - ipsec
  - networking
  - security
---
A friend pointed me recently to [a blog post](http://ciphergoth.livejournal.com/280821.html)
by [Paul Crowley](http://ciphergoth.livejournal.com/) discussing the major popular
cryptographic standards and some interesting proposals regarding their possible
replacement. At some point the question of whether network-layer or transport-layer
security systems are more appropriate was raised. The following is my opinion after
almost six years of research on information security and networking (more or less as
posted on that blog):

> There are many reasons to prefer transport-layer to network-layer security.
> Network-layer solutions need to be implemented in the operating system kernel making
> them particularly inconvenient to deploy. Also, IPsec (which for all practical purposes
> is the only network-layer security protocol we have) has been
> [widely criticized](http://www.schneier.com/paper-ipsec.html) for being exceptionally
> complex and this fact hinders in depth security evaluations. However, I think that the
> most important argument against network-layer security is that it violates basic
> networking stack architecture principles. When you are doing security management at
> the network layer it usually means that you lose all the reliability and reassembly
> features provided by the transport layer. To be able to make security decisions
> (like authentication, authorization, etc.) you need to re-implement many TCP features
> that allow you to assemble packets at the network layer, thus breaking the purpose
> behind the separation of functionality into layers.

The flexibility provided by IPsec is not a strong enough advantage to break the
abstraction borders between the different stack layers.
