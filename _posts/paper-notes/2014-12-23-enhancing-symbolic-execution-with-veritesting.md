---
id: 4864
title: Enhancing symbolic execution with veritesting
author: argp
layout: post
guid: http://sysc.tl/?p=4864
permalink: /2014/12/23/enhancing-symbolic-execution-with-veritesting/
categories:
  - paper notes
tags:
  - dynamic analysis
  - program analysis
  - static analysis
  - symbolic execution
  - veritesting
---
Title: Enhancing symbolic execution with veritesting  
PDF: <a href="http://cpl0.net/~argp/papers/2bf778fdcdfb9924adf057a79a9dc9a0.pdf" target="_blank">http://cpl0.net/~argp/papers/2bf778fdcdfb9924adf057a79a9dc9a0.pdf</a>

The core idea is the switching from dynamic symbolic execution to static (and vice-versa) when certain identified transition points are reached.

Example transition points from static to dynamic switching are unresolved jumps, system calls, function boundaries, and other cases that are easier to handle dynamically.