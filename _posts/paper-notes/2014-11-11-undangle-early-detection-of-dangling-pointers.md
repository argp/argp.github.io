---
id: 4621
title: 'Undangle: early detection of dangling pointers in use-after-free and double-free vulnerabilities'
author: argp
layout: post
guid: http://sysc.tl/?p=4621
permalink: /2014/11/11/undangle-early-detection-of-dangling-pointers/
categories:
  - paper notes
tags:
  - bitblaze
  - double-free
  - program analysis
  - taint tracking
  - temu
  - undangle
  - use-after-free
---
Title: Undangle: early detection of dangling pointers in use-after-free and double-free vulnerabilities  
PDF: <a href="http://cpl0.net/~argp/papers/881dc45d33c7bfea662a0889918999e4.pdf" target="_blank">http://cpl0.net/~argp/papers/881dc45d33c7bfea662a0889918999e4.pdf</a>

Uses <a href="http://bitblaze.cs.berkeley.edu/temu.html" target="_blank">TEMU</a> to produce an execution/allocations log which is then parsed offline; for each freed heap object the pointers to it are labeled as dangling; taint propagation-like techniques are used to track pointers.

Original Twitter link: <a href="https://twitter.com/_argp/statuses/505011997445193728" target="_blank">https://twitter.com/_argp/statuses/505011997445193728</a>