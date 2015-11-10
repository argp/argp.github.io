---
layout: post
title: "Paper notes: Enhancing symbolic execution with veritesting"
tags:
  - paper notes
  - dynamic analysis
  - program analysis
  - static analysis
  - symbolic execution
  - veritesting
---
Title: Enhancing symbolic execution with veritesting
PDF: <a href="/public/2bf778fdcdfb9924adf057a79a9dc9a0.pdf">2bf778fdcdfb9924adf057a79a9dc9a0.pdf</a>

The core idea is the switching from dynamic symbolic execution to static
(and vice-versa) when certain identified transition points are reached.

Example transition points from static to dynamic switching are unresolved
jumps, system calls, function boundaries, and other cases that are easier
to handle dynamically.
