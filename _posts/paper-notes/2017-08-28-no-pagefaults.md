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
knowledge of the source code of the attacked SGX application (in order to
monitor interesting page accesses).

The first attack exploits that accessed (and dirty) bits are set on pages
accessed/used by SGX application code in secure enclave mode. The page table
entry (PTE) attribute (accessed and/or dirty) that corresponds to the page
accessed in SGX mode is stored in the kernel memory of the unprotected system.

The second attack is based on cache misses; PTEs that refer to interesting
pages are evicted from the TLB (using `clflush`). When the enclave is
entered the TLB is cleared by design, therefore the attacker measures the
time required to reload the interesting PTEs when the enclave has returned.

Both attacks require the identification of interesting pages (and the
corresponding PTEs) in advance. There is an initial step in which the
attacked SGX application code is run outside the enclave, and a PC trace of
page accesses is recorded.

The authors have <a href="https://github.com/jovanbulck/sgx-pte">published
their implementation</a>, which I haven't tested, but from a quick pass
seems complete.
