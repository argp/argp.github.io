---
id: 223
title: Black Hat Europe 2010 update
author: argp
layout: post
guid: http://argp.gr/blog/?p=223
permalink: /2010/04/22/blackhat-eu-2010-update/
aktt_notify_twitter:
  - no
categories:
  - exploitation
  - freebsd
  - kernel
  - research
  - security
tags:
  - black hat
  - census
  - conference
  - exploitation
  - freebsd
  - kernel
  - research
  - security
---
[Black Hat Europe 2010][1] is now over and after a brief ash cloud caused delay I am back in Greece. It has been a great conference, flawlessly organised and with many outstanding presentations. I would like to thank everyone that attended my [presentation][2] but also all the kind people that spoke to me before and afterwards. I hope to meet all of you again at a future event.

[  
<img src="http://sysc.tl/wp-content/uploads/2010/04/bheu10_banner.png" alt="Black Hat Europe 2010" width="490" height="155" class="aligncenter size-full wp-image-231" />  
][1]

My presentation, titled &#8220;Binding the Daemon: FreeBSD Kernel Stack and Heap Exploitation&#8221;, was divided into four parts. In the first part I gave an overview of the published work on the subject of kernel exploitation for Unix-like operating systems. The second and third parts were the main body of the presentation. Specifically, in the second part I explained how a kernel stack overflow vulnerability on FreeBSD can be leveraged to achieve arbitrary code execution. The third part focused on a detailed security analysis of the Universal Memory Allocator (UMA), the FreeBSD kernel&#8217;s memory allocator. I explored how UMA overflows can lead to arbitrary code execution in the context of the latest stable FreeBSD kernel (8.0-RELEASE), and I developed an exploitation methodology for privilege escalation and kernel continuation.

In the fourth and final part I gave a demo of a FreeBSD kernel local 0day vulnerability that I have discovered. However, I have not released the details of the vulnerability in my Black Hat presentation. The details of this vulnerability (plus the proof-of-concept exploit) will be released shortly, once the relevant code is patched and the official advisory is out.

Below you may find all the material of my presentation, updated with some extra information and minor corrections:

  * Slides: [bheu-2010-slides.pdf][3]
  * White paper: [bheu-2010-wp.pdf][4]
  * Source code: bheu-2010-src.tar.gz</li> </ul>

 [1]: http://blackhat.com/html/bh-eu-10/bh-eu-10-home.html
 [2]: http://www.blackhat.com/html/bh-eu-10/bh-eu-10-archives.html#Argyroudis
 [3]: http://census-labs.com/media/bheu-2010-slides.pdf
 [4]: http://census-labs.com/media/bheu-2010-wp.pdf