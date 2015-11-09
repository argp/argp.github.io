---
id: 297
title: Windows and Windows CE port of the Stanford IBE library
author: argp
layout: post
guid: http://argp.gr/blog/?p=297
permalink: /2006/02/14/ibelib-win/
aktt_notify_twitter:
  - no
categories:
  - code
tags:
  - code
  - cryptography
  - ibe
  - windows
---
I recently ported the [Stanford IBE library][1] to Windows and Windows CE. You can get both ports from my [software projects page][2]. My Windows port builds natively using the MSVC++ development tools, while the one provided at the Stanford IBE page was cross-compiled for Windows with a Linux port of mingw and only includes the application binaries.

Note: On Windows CE the generation of the Solinas prime in the function IBE\_setup (file ibe\_lib.c) usually takes a couple of seconds.

 [1]: http://crypto.stanford.edu/ibe/
 [2]: http://ntrg.cs.tcd.ie/~argp/code/