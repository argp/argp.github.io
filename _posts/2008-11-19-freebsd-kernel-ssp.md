---
title: Kernel stack-smashing protection in FreeBSD-8.0-current-200811
layout: post
tags:
  - exploitation
  - exploitation mitigation
  - freebsd
  - kernel
  - memory corruption protection
  - propolice
  - ssp
---
Stack-smashing detection and protection for the kernel has been enabled by
default in the latest snapshot of FreeBSD 8.0-CURRENT
([200811](ftp://ftp.freebsd.org/pub/FreeBSD/snapshots/200811/)). This was
accomplished by utilizing the incorporation of
[SSP](http://www.trl.ibm.com/projects/security/ssp/) (also known as ProPolice)
in GCC version 4.1 and later (the 200811 snapshot uses GCC 4.2.1). 

Specifically, `src/sys/kern/stack_protector.c`, which is compiled with GCC's
`-fstack-protector` option, registers an event handler that generates a random
canary value (the "guard" variable in SSP terminology) placed between the local
variables and the saved frame pointer of a kernel process's stack during a
function's prologue. When the function exits, the canary is checked against its
original value. If it has been altered the kernel calls
[panic(9)](http://www.freebsd.org/cgi/man.cgi?query=panic&#038;apropos=0&#038;sektion=9&#038;manpath=FreeBSD+8-current&#038;format=html)
bringing down the whole system, but also stopping any execution flow redirection
caused by manipulation of the function's saved frame pointer or saved return address.

In contrast to StackGuard and StackShield (or even Microsoft's /GS), SSP has been
effective against attacks aiming to directly bypass it. This relates to
[research](http://rainbow.cs.unipi.gr/projects/oss/wiki/EventSixteen) I have done
in the near past on the subject of kernel stack-smashing attacks. However, SSP can
be indirectly bypassed by several methods, for example stack overflows on buffers
smaller than 8 bytes.
