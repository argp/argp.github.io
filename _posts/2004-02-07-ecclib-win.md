---
id: 265
title: ECC-LIB port for Windows and Windows CE
author: argp
layout: post
guid: http://argp.gr/blog/?p=265
permalink: /2004/02/07/ecclib-win/
aktt_notify_twitter:
  - no
categories:
  - code
tags:
  - code
  - cryptography
  - ecc
  - windows
---
I have ported the elliptic curve cryptography library ([ECC-LIB][1]) written by Elisavet Konstantinou, Yannis Stamatiou and Christos Zaroliagis to Windows and Windows CE. The actual package can be found on my [software projects page][2]. While you are there also get my port of GMP to Windows and Windows CE, which is required for the compilation and use of ECC-LIB. I have extensively tested both these ports on Windows XP and CE and I am satisfied with their stability. Unfortunately, I only have access to Compaq iPAQ H3630 (ARM) handhelds running the Windows CE (3.00) Pocket PC 2002 operating system. If you have any other handheld configuration running a different version of CE and test these ports, please let me know. At the moment I am working towards a detailed performance analysis of ECC-LIB on WinCE. I think that the comparison with some of [my previous results][3] will be very interesting.

 [1]: http://www.ceid.upatras.gr/faculty/zaro/software/ecc-lib/
 [2]: http://ntrg.cs.tcd.ie/~argp/code/
 [3]: http://ntrg.cs.tcd.ie/~argp/public/crypto-nca04.pdf