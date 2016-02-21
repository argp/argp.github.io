---
layout: post
title: "Paper notes: Towards automatic inference of kernel object semantics from binary code"
tags:
  - paper notes
  - program analysis
  - reverse engineering
---
Title: Towards automatic inference of kernel object semantics from binary code<br>
PDF: <a href="/public/63062e684afced0b70009b33d9ba7b26.pdf">63062e684afced0b70009b33d9ba7b26.pdf</a>

This is a runtime system that infers the types of kernel objects (data structures)
based on a) which system calls access an object, and b) how they access it (read,
write, create, delete). The implementation is based on a VMI (virtual machine
introspection) framework built on top of QEMU, and the presented results are
only for Linux kernels. A set of inference rules for Linux kernel data
structures must be manually defined. For example, an object created by
`sys_clone` and accessed for reading by `sys_getpid` is denoted as either
`task_struct` or `pid`. Therefore, the *automatic* claim of the title isn't
strictly applicable (at least according to my definition of *automatic*).
