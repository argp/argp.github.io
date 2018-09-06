---
layout: post
title: "Paper notes: HeapHopper"
tags:
  - paper notes
  - heap metadata exploitation
  - symbolic execution
  - model checking
  - angr
  - ptmalloc
  - dlmalloc
---
Title: HeapHopper: Bringing bounded model checking to heap implementation security<br>
PDF: <a href="/public/970a2d1ce20edee6eaf3b9cecd071f81.pdf">970a2d1ce20edee6eaf3b9cecd071f81.pdf</a>

A system for evaluating heap allocator implementations for metadata corruption
attacks. Comes with <a href="https://github.com/angr/heaphopper">an open source implementation</a>,
and it uses <a href="https://github.com/angr/angr">angr</a> to analyze the binaries that implement the
target allocator. A configuration file is also required to specify the attackers capabilities;
the heap operations she can perform (malloc, free), but also higher level attack primitives,
like heap buffer overflows, use-after-frees, double frees, and arbitrary frees. The configuration
file also includes a list of states corresponding to violated security properties (i.e. exploitation
primitives). For example, a return-used primitive (or "overlapping allocation" as the authors call
it) is checked when a new allocation is made with malloc returning address A, by using an SMT solver
to check if the following holds (B is the address of an already used allocation):

∃B : ((A ≤ B) ∧ (A + sizeof(A) > B)) ∨ ((A ≥ B) ∧ (B + sizeof(B) > A))

The corresponding Python angr code for the above check can be found
<a href="https://github.com/angr/heaphopper/blob/master/heaphopper/analysis/heap_condition_tracker.py#L205">here</a>.

Based on the configuration file, series of C programs are produced, compiled, and symbolically
executed against the target allocator. Using angr, the allocator's malloc and free functions are
hooked and monitored for the security violations described in the configuration file. The symbolic
execution traces and the associated constraints are finally used to create the next series of C
programs, until the specified exploitation primitives are achieved. The paper includes a detailed
evaluation section for the dlmalloc and ptmalloc allocators. I didn't have the time yet to play
with HeapHopper's code, but I plan to test it against jemalloc; I'll be posting my findings here
when I do so.
