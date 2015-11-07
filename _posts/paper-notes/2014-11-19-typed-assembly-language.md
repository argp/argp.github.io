---
id: 4633
title: Toward a foundational typed assembly language
author: argp
layout: post
guid: http://sysc.tl/?p=4633
permalink: /2014/11/19/typed-assembly-language/
categories:
  - paper notes
tags:
  - assembly
  - OCaml
  - reasoning
  - TAL
  - TALx86
  - type checking
  - type system
  - verification
  - x86
---
Title: Toward a foundational typed assembly language  
PDF: <a href="http://cpl0.net/~argp/papers/7b0f643010e5537ff02debab6b2fce4b.pdf" target="_blank">http://cpl0.net/~argp/papers/7b0f643010e5537ff02debab6b2fce4b.pdf</a>

A paper from 2002 but a very interesting read; it formally defines a type system for a complete assembly language (TAL). The paper gives typing rules for the instructions and for memory allocation; its advantages are verification and reasoning (for things like heap object reachability) with machine-checked proofs.

An implementation (in OCaml) of TAL for x86 is <a href="http://www.cs.cornell.edu/talc/releases.html" target="_blank">TALx86</a>; includes a type-checker and an assembler.

Original Twitter link: <a href="https://twitter.com/_argp/statuses/524588812731969536" target="_blank">https://twitter.com/_argp/statuses/524588812731969536</a>