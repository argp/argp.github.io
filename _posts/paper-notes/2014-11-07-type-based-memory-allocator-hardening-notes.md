---
title: "Paper notes: Type-based memory allocator hardening notes"
layout: post
tags:
  - paper notes
  - isolated heap
  - memory allocator hardening
  - type-safety
---
Internet Explorer's new `g_hIsolatedHeap` mitigation is like a poor man's
type-safe memory reuse implementation. "Poor man's" since instead of real
type-safety, it specifies categories of "dangerous" objects that are placed
on the isolated heap. An example full implementation of type-safe memory
reuse is <a href="/public/3f7f268d4896869a6634f76403e5954b.pdf">Cling</a>,
a heap manager that restricts memory reuse to same-type objects.

Of course
<a href="http://robert.ocallahan.org/2010/10/mitigating-dangling-pointer-bugs-using_15.html">Firefox's
frame poisoning</a> (since 2010) also implements some type-safe memory reuse
ideas.

Btw, the above frame poisoning blog post does not refer to Cling, but a
<a href="/public/a8f45baeab77e1bf41d30dce444523b3.pdf">much earlier paper</a>
on type-safe memory reuse.

Relevant Twitter link:
<a href="https://twitter.com/_argp/statuses/498798680863145984">https://twitter.com/_argp/statuses/498798680863145984</a>
