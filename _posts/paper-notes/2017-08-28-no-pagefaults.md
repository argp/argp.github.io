---
layout: post
title: "Paper notes: Telling your secrets without page faults"
tags:
  - paper notes
  - sgx attacks
  - side-channel attacks
---
Title: Telling your secrets without page faults<br>
PDF: <a href="/public/b81efa3a4c5826fa441852bd63a402c6.pdf">b81efa3a4c5826fa441852bd63a402c6.pdf</a>

A paper on two attacks against Intel SGX enclaves using side-effects of
page table walks, without explicitly observing page faults. Both attacks
are based on the fact that when the processor is in enclave execution mode,
it still accesses the page table which is in unprotected (i.e. non-SGX) memory.
SGX defines some access control mechanisms on top of that, but they don't
hinder the presented attacks.

The threat model under which the attacks are developed assumes a completely
attacker-controlled operating system (both userland and kernel), and
knowledge of the source code of the attacked SGX application.

The first attack is based on accessed and dirty bits 

The second attack uses the 
