---
title: Pseudomonarchia jemallocum
layout: post
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
[Phrack 0x44](http://www.phrack.org/issues/68/1.html)
is out with my and huku's research on exploiting
[jemalloc](http://www.canonware.com/jemalloc/) titled:

[Pseudomonarchia jemallocum: The false kingdom of jemalloc, or on exploiting the
jemalloc memory manager](http://www.phrack.org/issues/68/10.html#article)

I have been working on and off jemalloc since mid 2010 and it's very nice to
see the work published. In [Phrack](http://www.phrack.org/) :)

As the main paper mentions, the development of our gdb/Python utility
`unmask_jemalloc` will continue on
[GitHub](https://github.com/argp/unmask_jemalloc).
