---
id: 350
title: Short Black Hat Europe 2011 review
author: argp
layout: post
guid: http://argp.gr/blog/?p=350
permalink: /2011/03/21/short-bheu2011-review/
aktt_notify_twitter:
  - no
categories:
  - security
tags:
  - black hat
  - conference
---
I am not really the kind of person that writes conference reviews, but I will give you a short, almost telegraphical one of [this year&#8217;s Black Hat Europe][1].

### Day 1

Contrary to conference tradition, day 1 begun without a keynote as Bruce Schneier was unable to be in Barcelona in the morning. The first talk I attended was Nitesh Dhanjani&#8217;s &#8220;New Age Attacks Against Apple&#8217;s iOS&#8221;. This talk mainly focused on abusing mobile Safari&#8217;s protocol handlers and, although well delivered, wasn&#8217;t that interesting to me. Next was Tom Keetch&#8217;s &#8220;Escaping From Microsoft Windows Sandboxes&#8221; in which Tom gave an overview of the Windows sandbox implementation, and explained how Internet Explorer, Google Chrome and Adobe Reader X use it. Furthermore, he presented mechanisms for bypassing the Windows sandbox both generically and specific to the above applications. I really liked this talk and it is my second choice for best talk of day 1. Then I presented mine and Dimitris Glynos&#8217; &#8220;Protecting the Core&#8221; talk; I got some nice feedback which we will incorporate in the updated version of the slide deck. Next was Mihai Chiriac&#8217;s &#8220;Rootkit Detection via Kernel Code Tunneling&#8221;, an interesting approach for detecting kernel rootkits on Windows with lightweight heuristic analysis and interesting features for live-system disinfection. The final talk of the day was also the best one, Chris Valasek&#8217;s and Ryan Smith&#8217;s &#8220;Exploitation in the Modern Era&#8221;. They successfully tried to abstract the process of exploitation into building blocks, or primitives according to the terminology they used in the talk, and how these building blocks were used during the development of two server-side Windows exploits. Day 1 ended with Bruce Schneier&#8217;s keynote on cyber war incidents, how countries prepare (or not) for it, and how cyber war will eventually and inevitably become part of all military confrontations.

### Day 2

Day 2 started with an amazing talk, Sebastian Muniz&#8217;s and Alfredo Ortega&#8217;s &#8220;Fuzzing and Debugging Cisco IOS&#8221;. These two highly talented and competent researchers explained their setup and modifications to the Dynamips emulator for debugging, reversing and fuzzing IOS. Then I went to Tom Parker&#8217;s &#8220;Stuxnet Redux&#8221; talk, but I left after 20 minutes or so since the talk was too abstract and non-technical for my taste. I was able to attend the last 30 minutes of George Hedfors&#8217; &#8220;Owning the data centre using Cisco NX-OS based switches&#8221;. George explained how he was able to break out of the restrictive shell of Cisco&#8217;s NX (which is Linux-based), as well as how the old CDP denial-of-service bug is unpatched on NX. FX&#8217;s &#8220;Building Custom Disassemblers&#8221; was, as I expected, nothing short of brilliant. He documented step-by-step the process of building a custom disassembler for the binary code of a certain Siemens microcontroller. At the end of the talk he revealed that this was actually one of the microcontrollers that Stuxnet was carrying code to attack. To be honest, the Stuxnet connection was not the interesting part of the talk (although it was fun). The insight on FX&#8217;s work process, and his tips and approaches on reverse engineering were the most interesting parts for me. I then attended Don Bailey&#8217;s &#8220;Attacking Microcontroller Environments from a Software Perspective&#8221;. Apart from the investment tips, he also gave us exploitation methodologies for attacking two different microcontrollers, one of the von Neumann and one of the Harvard architecture. The day ended with Vincenzo Iozzo&#8217;s &#8220;Mac Exploit Kitchen&#8221; workshop which was great fun.

In closing I would say that when compared to [2010][2], this year&#8217;s Black Hat Europe had more interesting (to me) talks. It was my second Black Hat Europe as a presenter in a row and it was great meeting new people as well as seeing those I met last year.

In between the technical sessions and after them I partied non-stop. The partying was hot.

Yes, I am being sarcastic. I am a nerd. I don&#8217;t go out much actually.

 [1]: https://www.blackhat.com/html/bh-eu-11/bh-eu-11-home.html
 [2]: http://argp.gr/blog/2010/04/22/blackhat-eu-2010-update/