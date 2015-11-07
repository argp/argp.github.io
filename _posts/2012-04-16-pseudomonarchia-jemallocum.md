---
id: 601
title: Pseudomonarchia jemallocum
author: argp
layout: post
guid: http://sysc.tl/blog/?p=601
permalink: /2012/04/16/pseudomonarchia-jemallocum/
aktt_notify_twitter:
  - no
categories:
  - code
  - exploitation
  - freebsd
  - linux
  - os x
  - research
  - security
tags:
  - code
  - exploitation
  - firefox
  - freebsd
  - heap
  - jemalloc
  - netbsd
  - phrack
  - userland heap
---
[Phrack 0x44][1] is out with my and [huku][2]&#8216;s research on exploiting [jemalloc][3] titled:

[&#8220;Pseudomonarchia jemallocum: The false kingdom of jemalloc, or on exploiting the jemalloc memory manager&#8221;][4]

I have been working on and off jemalloc since mid 2010 and it&#8217;s very nice to see the work published. In Phrack :)

As the main paper mentions, the development of our gdb/Python utility `unmask_jemalloc` will continue on [github][5].

 [1]: http://phrack.org/issues.html?issue=68
 [2]: http://dp.grhack.net/
 [3]: http://www.canonware.com/jemalloc/
 [4]: http://phrack.org/issues.html?issue=68&#038;id=10#article
 [5]: https://github.com/argp/unmask_jemalloc