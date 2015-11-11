---
title: "Paper notes: Undangle: early detection of dangling pointers in use-after-free and double-free vulnerabilities"
layout: post
tags:
  - paper notes
  - bitblaze
  - double-free
  - program analysis
  - taint tracking
  - temu
  - undangle
  - use-after-free
---
Title: Undangle: early detection of dangling pointers in use-after-free
and double-free vulnerabilities <br>
PDF: <a href="/public/881dc45d33c7bfea662a0889918999e4.pdf">881dc45d33c7bfea662a0889918999e4.pdf</a>

Uses <a href="http://bitblaze.cs.berkeley.edu/temu.html">TEMU</a> to produce
an execution/allocations log which is then parsed offline; for each freed heap
object the pointers to it are labeled as dangling; taint propagation-like
techniques are used to track pointers.

Original Twitter link:
<a href="https://twitter.com/_argp/statuses/505011997445193728">https://twitter.com/_argp/statuses/505011997445193728</a>
