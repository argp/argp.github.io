---
title: "Paper notes: Memory leak detection based on memory state transition graph"
layout: post
tags:
  - paper notes
  - memory leak detection
  - program analysis
  - static analysis
---
Title: Memory leak detection based on memory state transition graph<br>
PDF: <a href="/public/9d850ea1ce88e3705bd40b56164a6f40.pdf">9d850ea1ce88e3705bd40b56164a6f40.pdf</a>

Memory state transition graph (MSTG) nodes model heap objects' states; edges are
annotated with path conditions (via symbolic execution); used for function
summaries and the leak detection algorithm.

Implementation (just binaries, no source code) available at:
<a href="http://lcs.ios.ac.cn/~xuzb/melton.html">http://lcs.ios.ac.cn/~xuzb/melton.html</a>

Relevant Twitter link:
<a href="https://twitter.com/_argp/statuses/490102227819053056">https://twitter.com/_argp/statuses/490102227819053056</a>
