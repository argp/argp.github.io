---
id: 16
title: netris hack
author: argp
layout: post
guid: http://argp.gr/blog/?p=16
permalink: /2007/04/23/netris-hack/
categories:
  - code
  - hacks
tags:
  - code
  - netris
---
[This patch][1] I coded against [netris version 0.52][2] allows you to send junk rows to your opponent. The default key to do this is `h` and the default number of rows to send is `1`. You can change the former by remapping the keys (with the `-k` switch) and the latter with the new `-j` switch (see the output of `netris -h` for more details). Have fun and don&#8217;t be too mean.

 [1]: http://ntrg.cs.tcd.ie/~argp/code/netris-0.52-argp-hack.diff
 [2]: ftp://ftp.netris.org/pub/netris/netris-0.52.tar.gz