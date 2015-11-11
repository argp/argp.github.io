---
layout: post
title: "Paper notes: A first step towards automated detection of buffer overrun vulnerabilities"
tags:
  - paper notes
  - boon
  - program analysis
  - range solver
  - static analysis
---
Title: A first step towards automated detection of buffer overrun vulnerabilities (BOON)<br>
PDF: <a href="/public/24dcd918253f6a44a43ac6612294397f.pdf">24dcd918253f6a44a43ac6612294397f.pdf</a>

I was looking at BOON lately and it has a nice integrated and reusable range
solver to check constraints for integer variables. Much faster and scalable
than an SMT solver, although imprecise since it is path insensitive.

See <a href="http://www.cs.berkeley.edu/~daw/boon/">BOON's implementation</a>
for the range solver; specifically files `boon-1.0/{newsolver.c, constraint-set.sml}`.

Original Twitter link:
<a href="https://twitter.com/_argp/statuses/512231214153871360">https://twitter.com/_argp/statuses/512231214153871360</a>
