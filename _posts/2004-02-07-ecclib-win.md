---
title: ECC-LIB port for Windows and Windows CE
layout: post
tags:
  - code
  - cryptography
  - ecc
  - windows
---
I have ported the elliptic curve cryptography library
([ECC-LIB](http://www.ceid.upatras.gr/faculty/zaro/software/ecc-lib/)) written
by Elisavet Konstantinou, Yannis Stamatiou and Christos Zaroliagis to
[Windows](https://github.com/argp/ecc-lib-win32) and
[Windows CE](https://github.com/argp/ecc-lib-wince). You also need to get my port
of GMP to [Windows](https://github.com/argp/gmp-win32) and
[Windows CE](https://github.com/argp/gmp-wince), which is required for the
compilation and use of ECC-LIB.

I have extensively tested both these ports on Windows XP and CE and I am satisfied
with their stability. Unfortunately, I only have access to Compaq iPAQ H3630 (ARM)
handhelds running the Windows CE (3.00) Pocket PC 2002 operating system. If you
have any other handheld configuration running a different version of CE and test
these ports, please let me know. At the moment I am working towards a detailed
performance analysis of ECC-LIB on WinCE. I think that the comparison with some of
[my previous results](/public/crypto-nca04.pdf) will be very interesting.
