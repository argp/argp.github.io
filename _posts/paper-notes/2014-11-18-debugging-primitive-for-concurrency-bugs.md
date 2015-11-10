---
title: "Paper notes: Time-ordered event traces: a new debugging primitive for concurrency bugs"
layout: post
tags:
  - paper notes
  - concurrency
  - concurrency bugs
  - debugging
  - root cause analysis
---
Title: Time-ordered event traces: a new debugging primitive for concurrency bugs<br>
PDF: <a href="/public/4feb0d2508fcab1061401f6212dde8a2.pdf">4feb0d2508fcab1061401f6212dde8a2.pdf</a>

A methodology and
<a href="http://people.engr.ncsu.edu/hzhou/TracesWeb/download.html">accompanying pintool</a> for
root cause analysis of concurrency bugs; it basically records a runtime trace of function calls
and returns, their thread IDs and global timestamps, making clear the order in which they execute.

I really liked that the paper includes five case studies, one of which demonstrates a shortcoming
of the approach (a quite common one however).

Original Twitter link:
<a href="https://twitter.com/_argp/statuses/521674700683223041">https://twitter.com/_argp/statuses/521674700683223041</a>
