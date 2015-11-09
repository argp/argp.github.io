---
id: 4627
title: 'Time-ordered event traces: a new debugging primitive for concurrency bugs'
author: argp
layout: post
guid: http://sysc.tl/?p=4627
permalink: /2014/11/18/debugging-primitive-for-concurrency-bugs/
dsq_thread_id:
  - 3791915577
categories:
  - paper notes
tags:
  - concurrency
  - concurrency bugs
  - debugging
  - root cause analysis
---
Title: Time-ordered event traces: a new debugging primitive for concurrency bugs  
PDF: <a href="http://cpl0.net/~argp/papers/4feb0d2508fcab1061401f6212dde8a2.pdf" target="_blank">http://cpl0.net/~argp/papers/4feb0d2508fcab1061401f6212dde8a2.pdf</a>

A methodology and <a href="http://people.engr.ncsu.edu/hzhou/TracesWeb/download.html" target="_blank">accompanying pintool</a> for root cause analysis of concurrency bugs; it basically records a runtime trace of function calls and returns, their thread IDs and global timestamps, making clear the order in which they execute.

I really liked that the paper includes five case studies, one of which demonstrates a shortcoming of the approach (a quite common one however).

Original Twitter link: <a href="https://twitter.com/_argp/statuses/521674700683223041" target="_blank">https://twitter.com/_argp/statuses/521674700683223041</a>