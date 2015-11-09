---
id: 86
title: kernel stack-smashing protection in freebsd-8.0-current-200811
author: argp
layout: post
guid: http://argp.gr/blog/?p=86
permalink: /2008/11/19/freebsd-kernel-ssp/
categories:
  - exploitation
  - freebsd
  - kernel
  - research
tags:
  - exploitation
  - exploitation mitigation
  - freebsd
  - kernel
  - memory corruption protection
  - propolice
  - ssp
---
Stack-smashing detection and protection for the kernel has been enabled by default in the latest snapshot of FreeBSD 8.0-CURRENT ([200811][1]). This was accomplished by utilizing the incorporation of [SSP][2] (also known as ProPolice) in gcc version 4.1 and later (the 200811 snapshot uses gcc 4.2.1). 

Specifically, `src/sys/kern/stack_protector.c`, which is compiled with gcc&#8217;s `-fstack-protector` option, registers an event handler that generates a random canary value (the &#8220;guard&#8221; variable in SSP terminology) placed between the local variables and the saved frame pointer of a kernel process&#8217;s stack during a function&#8217;s prologue. When the function exits, the canary is checked against its original value. If it has been altered the kernel calls [panic(9)][3] bringing down the whole system, but also stopping any execution flow redirection caused by manipulation of the function&#8217;s saved frame pointer or saved return address.

In contrast to StackGuard and StackShield (or even Microsoft&#8217;s /GS), SSP has been effective against attacks aiming to directly bypass it. This relates to [research][4] I have done in the near past on the subject of kernel stack-smashing attacks. However, SSP can be indirectly bypassed by several methods, for example heap overflows, integer and/or signedness vulnerabilities, and stack overflows on buffers smaller than 8 bytes, among others.

 [1]: ftp://ftp.freebsd.org/pub/FreeBSD/snapshots/200811/
 [2]: http://www.trl.ibm.com/projects/security/ssp/
 [3]: http://www.freebsd.org/cgi/man.cgi?query=panic&#038;apropos=0&#038;sektion=9&#038;manpath=FreeBSD+8-current&#038;format=html
 [4]: http://rainbow.cs.unipi.gr/projects/oss/wiki/EventSixteen