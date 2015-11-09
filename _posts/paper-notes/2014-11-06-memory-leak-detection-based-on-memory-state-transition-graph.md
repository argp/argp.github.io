---
id: 4598
title: Memory leak detection based on memory state transition graph
author: argp
layout: post
guid: http://sysc.tl/?p=4598
permalink: /2014/11/06/memory-leak-detection-based-on-memory-state-transition-graph/
categories:
  - paper notes
tags:
  - memory leak detection
  - program analysis
  - static analysis
---
Title: Memory leak detection based on memory state transition graph  
PDF: <a href="http://cpl0.net/~argp/papers/9d850ea1ce88e3705bd40b56164a6f40.pdf" target="_blank">http://cpl0.net/~argp/papers/9d850ea1ce88e3705bd40b56164a6f40.pdf</a>

Memory state transition graph (MSTG) nodes model heap objects&#8217; states; edges are annotated with path conditions (via symbolic execution); used for function summaries and the leak detection algorithm.

Implementation (just binaries, no source code) available at: <a href="http://lcs.ios.ac.cn/~xuzb/melton.html" target="_blank">http://lcs.ios.ac.cn/~xuzb/melton.html</a>

Relevant Twitter link: <a href="https://twitter.com/_argp/statuses/490102227819053056" target="_blank">https://twitter.com/_argp/statuses/490102227819053056</a>