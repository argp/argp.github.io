---
title: FreeBSD kernel stack overflows
layout: post
tags:
  - exploitation
  - freebsd
  - kernel
---
Last May (2008/05/30) I presented my research on FreeBSD kernel stack overflows 
at the <a href="http://rainbow.cs.unipi.gr/projects/oss/wiki/EventSixteen" 
target="blank">University of Piraeus Software Libre Society, Event #16: 
Computer Security</a>. The slides from my talk are now available from the 
[research section][1] of the [census][2] web page.

In the talk I explored in detail the process of exploiting kernel stack 
overflows in the 7.0 production release of the <a 
href="http://www.freebsd.org/" target="blank">FreeBSD</a> operating system. 
There were extensive examples and live experimentation, all of which are 
unfortunately not reflected in the supporting slides. The main contribution of 
the study is the development of a kernel exploitation algorithm and the 
presentation of comprehensive i386 kernel shellcode. Although the focus was on 
the then most current production release of FreeBSD (7.0), the presented 
algorithm and methodologies are applicable to both the latest stable (7.1) and 
current (8.0) FreeBSD versions.

 [1]: http://census-labs.com/research/
 [2]: http://census-labs.com/
