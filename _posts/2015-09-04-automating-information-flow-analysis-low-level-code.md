---
layout: post
title: Paper notes: Automating information flow analysis of low level code
tags:
  - paper notes
  - program analysis
  - symbolic execution
  - verification
---
Title: Automating information flow analysis of low level code<br>
PDF: <a href="http://cpl0.net/~argp/papers/68d4b37e9623d0c67e7b856b76ebe4a1.pdf" target="_blank">http://cpl0.net/~argp/papers/68d4b37e9623d0c67e7b856b76ebe4a1.pdf</a>

Uses BAP to lift ARMv7 code to BIL (BAP's intermediate representation language) with the <a href="http://hol-theorem-prover.org/">HOL4 model of ARMv7</a> and does forward symbolic execution to build a logical formula that describes several executions. At interesting execution points (called observation points in the paper), such as writes, offloading to SMT solving is used to verify that relational properties hold. Loops are handled by manually finding relational invariants and using them to decorate the loops aiding the verification.
