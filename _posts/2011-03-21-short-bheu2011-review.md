---
title: Short Black Hat Europe 2011 review
layout: post
tags:
  - black hat
  - conference
---
I am not really the kind of person that writes conference reviews, but I will
give you a short, almost telegraphical one of [this year's Black Hat
Europe](https://www.blackhat.com/html/bh-eu-11/bh-eu-11-home.html).

### Day 1

Contrary to conference tradition, day 1 begun without a keynote as Bruce
Schneier was unable to be in Barcelona in the morning. The first talk I attended
was Nitesh Dhanjani's "New Age Attacks Against Apple's iOS". This talk mainly
focused on abusing mobile Safari's protocol handlers and, although well
delivered, wasn't that interesting to me. Next was Tom Keetch's "Escaping From
Microsoft Windows Sandboxes" in which Tom gave an overview of the Windows
sandbox implementation, and explained how Internet Explorer, Google Chrome and
Adobe Reader X use it. Furthermore, he presented mechanisms for bypassing the
Windows sandbox both generically and specific to the above applications. I
really liked this talk and it is my second choice for best talk of day 1. Then I
presented mine and Dimitris Glynos' "Protecting the Core" talk; I got some nice
feedback which we will incorporate in the updated version of the slide deck.
Next was Mihai Chiriac's "Rootkit Detection via Kernel Code Tunneling", an
interesting approach for detecting kernel rootkits on Windows with lightweight
heuristic analysis and interesting features for live-system disinfection. The
final talk of the day was also the best one, Chris Valasek's and Ryan Smith's
"Exploitation in the Modern Era". They successfully tried to abstract the
process of exploitation into building blocks, or primitives according to the
terminology they used in the talk, and how these building blocks were used
during the development of two server-side Windows exploits. Day 1 ended with
Bruce Schneier's keynote on cyber war incidents, how countries prepare (or not)
for it, and how cyber war will eventually and inevitably become part of all
military confrontations.

### Day 2

Day 2 started with an amazing talk, Sebastian Muniz's and Alfredo Ortega's
"Fuzzing and Debugging Cisco IOS". These two highly talented and competent
researchers explained their setup and modifications to the Dynamips emulator for
debugging, reversing and fuzzing IOS. Then I went to Tom Parker's "Stuxnet
Redux" talk, but I left after 20 minutes or so since the talk was too abstract
and non-technical for my taste. I was able to attend the last 30 minutes of
George Hedfors' "Owning the data centre using Cisco NX-OS based switches".
George explained how he was able to break out of the restrictive shell of
Cisco's NX (which is Linux-based), as well as how the old CDP denial-of-service
bug is unpatched on NX. FX's "Building Custom Disassemblers" was, as I expected,
nothing short of brilliant. He documented step-by-step the process of building a
custom disassembler for the binary code of a certain Siemens microcontroller. At
the end of the talk he revealed that this was actually one of the
microcontrollers that Stuxnet was carrying code to attack. To be honest, the
Stuxnet connection was not the interesting part of the talk (although it was
fun). The insight on FX's work process, and his tips and approaches on reverse
engineering were the most interesting parts for me. I then attended Don Bailey's
"Attacking Microcontroller Environments from a Software Perspective". Apart from
the investment tips, he also gave us exploitation methodologies for attacking
two different microcontrollers, one of the von Neumann and one of the Harvard
architecture. The day ended with Vincenzo Iozzo's "Mac Exploit Kitchen" workshop
which was great fun.

In closing I would say that when compared to
[2010](https://argp.github.io/2010/04/22/blackhat-eu-2010-update/), this year's
Black Hat Europe had more interesting (to me) talks. It was my second Black Hat
Europe as a presenter in a row and it was great meeting new people as well as
seeing those I met last year.

In between the technical sessions and after them I partied non-stop. The
partying was hot.

Yes, I am being sarcastic. I am a nerd. I don't go out much actually.
