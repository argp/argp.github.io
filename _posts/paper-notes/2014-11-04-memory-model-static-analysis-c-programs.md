---
id: 4592
title: A memory model for static analysis of C programs
author: argp
layout: post
guid: http://sysc.tl/?p=4592
permalink: /2014/11/04/memory-model-static-analysis-c-programs/
categories:
  - paper notes
tags:
  - memory model
  - program analysis
  - static analysis
---
Title: A memory model for static analysis of C programs  
PDF: <a href="http://cpl0.net/~argp/papers/44f93d2a09e3d91eca160b387db6cd8c.pdf" target="_blank">http://cpl0.net/~argp/papers/44f93d2a09e3d91eca160b387db6cd8c.pdf</a>

Nice read; defines a region-based memory model that can describe C semantics and keep track of lvalue expressions; like a poor man&#8217;s alias analysis. Implementation available as part of the clang analyzer.

Original Twitter link: <a href="https://twitter.com/_argp/statuses/483678143371550720" target="_blank">https://twitter.com/_argp/statuses/483678143371550720</a>