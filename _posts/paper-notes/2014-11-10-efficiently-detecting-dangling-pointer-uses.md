---
id: 4610
title: Efficiently detecting all dangling pointer uses in production servers
author: argp
layout: post
guid: http://sysc.tl/?p=4610
permalink: /2014/11/10/efficiently-detecting-dangling-pointer-uses/
categories:
  - paper notes
tags:
  - dangling pointers
  - dynamic analysis
  - pageheap
  - program analysis
---
Title: Efficiently detecting all dangling pointer uses in production servers  
PDF: <a href="http://cpl0.net/~argp/papers/5f11226846ef1fb1e447ca58fbba6d33.pdf" target="_blank">http://cpl0.net/~argp/papers/5f11226846ef1fb1e447ca58fbba6d33.pdf</a>

Runtime detection by placing each allocated object on a new virtual page (like pageheap), but mapping multiple virtual pages to the same physical page avoiding physical memory depletion.

Freed objects cause an mprotect on their page, so possible later uses of the object cause an access violation in turn. Implemented as LLVM IR transformation; tested via C -> IR -> transformations -> IR&#8217; -> C&#8217; -> gcc -O3 :)

Original Twitter link: <a href="https://twitter.com/_argp/statuses/499961355097866241" target="_blank">https://twitter.com/_argp/statuses/499961355097866241</a>