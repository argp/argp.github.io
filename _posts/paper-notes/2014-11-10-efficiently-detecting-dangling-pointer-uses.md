---
title: "Paper notes: Efficiently detecting all dangling pointer uses in production servers"
layout: post
tags:
  - paper notes
  - dangling pointers
  - dynamic analysis
  - pageheap
  - program analysis
---
Title: Efficiently detecting all dangling pointer uses in production servers<br>
PDF: <a href="/public/5f11226846ef1fb1e447ca58fbba6d33.pdf">5f11226846ef1fb1e447ca58fbba6d33.pdf</a>

Runtime detection by placing each allocated object on a new virtual page
(like pageheap), but mapping multiple virtual pages to the same physical
page avoiding physical memory depletion.

Freed objects cause an mprotect on their page, so possible later uses of
the object cause an access violation in turn. Implemented as LLVM IR
transformation; tested via
`C -> IR -> transformations -> IR' -> C' -> gcc -O3` :)

Original Twitter link:
<a href="https://twitter.com/_argp/statuses/499961355097866241">https://twitter.com/_argp/statuses/499961355097866241</a>
