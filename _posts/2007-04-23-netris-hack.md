---
title: netris hack
layout: post
tags:
  - code
  - netris
  - hack
---
[This patch](/public/netris-0.52-argp-hack.patch) I coded against
[netris version
0.52](http://http.debian.net/debian/pool/main/n/netris/netris_0.52.orig.tar.gz)
allows you to send junk rows to your opponent. The default key to do this is `h`
and the default number of rows to send is `1`. You can change the former by
remapping the keys (with the `-k` switch) and the latter with the new `-j` switch
(see the output of `netris -h` for more details).

Have fun and don't be too mean.
