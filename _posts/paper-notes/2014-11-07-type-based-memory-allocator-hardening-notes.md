---
id: 4601
title: Type-based memory allocator hardening notes
author: argp
layout: post
guid: http://sysc.tl/?p=4601
permalink: /2014/11/07/type-based-memory-allocator-hardening-notes/
categories:
  - paper notes
tags:
  - isolated heap
  - memory allocator hardening
  - type-safety
---
Internet Explorer&#8217;s new g_hIsolatedHeap mitigation is like a poor man&#8217;s type-safe memory reuse implementation. &#8220;Poor man&#8217;s&#8221; since instead of real type-safety, it specifies categories of &#8220;dangerous&#8221; objects that are placed on the isolated heap. An example full implementation of type-safe memory reuse is <a href="http://cpl0.net/~argp/papers/3f7f268d4896869a6634f76403e5954b.pdf" target="_blank">Cling</a>, a heap manager that restricts memory reuse to same-type objects.

Of course <a href="http://robert.ocallahan.org/2010/10/mitigating-dangling-pointer-bugs-using_15.html" target="_blank">Firefox&#8217;s frame poisoning</a> (since 2010) also implements some type-safe memory reuse ideas.

Btw, the above frame poisoning blog post does not refer to Cling, but a <a href="http://cpl0.net/~argp/papers/a8f45baeab77e1bf41d30dce444523b3.pdf" target="_blank">much earlier paper</a> on type-safe memory reuse.

Relevant Twitter link: <a href="https://twitter.com/_argp/statuses/498798680863145984" target="_blank">https://twitter.com/_argp/statuses/498798680863145984</a>