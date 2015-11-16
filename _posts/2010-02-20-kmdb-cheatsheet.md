---
title: Quick kmdb cheatsheet
layout: post
tags:
  - debugging
  - kernel
  - kmdb
  - opensolaris
  - solaris
---
This is mainly a reference for myself since I have been playing with OpenSolaris
kernel internals lately:

* To enable kmdb edit the kernel's grub entry and append `-k` to it.
* Break into kmdb: `f1+a`
* Display status: `::status`
* List available kmdb commands (and be amazed): `::dcmds`
* View registers for CPU 0: `::cpuregs -c 0` and/or `::regs`
* Set a breakpoint at the given symbol or address: `::bp [symbol or address]`
* Set a read/write watchpoint at the given symbol or address:
  `[symbol or address] ::wp -rw`
* Display breakpoints and watchpoints: `::events`
* Delete breakpoint (or watchpoint) #1: `::delete 1`
* Continue execution: `:c`
* Next instruction, step into function calls: `::step`
* Next instruction, step over function calls: `::step over`
* Return from current function: `::step out`
* Continue execution until the next branching instruction (only x86):
  `::step branch`
* Disassemble around RIP: `<rip::dis`
* Disassemble 100 instructions starting at the given symbol or address:
  `::dis -n 100 [symbol or address]`
* View backtrace: `$C`
* View IDT: `::idt`
* View symbols: `::nm`
* View the kernel message buffer: `::msgbuf`
* Quit kmdb and reboot: `::quit` </ul>

This brief cheatsheet does not do kmdb justice; it is an amazing built-in kernel
debugger with countless features. For more details [read the
manpage](https://docs.oracle.com/cd/E36784_01/html/E36870/kmdb-1.html).
