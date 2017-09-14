---
layout: post
title: "Paper notes: Reverse engineering x86 processor microcode"
tags:
  - paper notes
  - reverse engineering
  - x86 microcode
  - amd k10
---
Title: Reverse engineering x86 processor microcode<br>
PDF: <a href="/public/133f02627cbd3771ad5d4b09729cfce7.pdf">133f02627cbd3771ad5d4b09729cfce7.pdf</a>

A very interesting paper with technical details on the x86 microcode inner
workings of AMD's K8 and K10 CPUs. The reason for focusing on these old CPUs
is that other/newer ones cryptographically protect their microcode updates,
both for authenticity/integrity and confidentiality.

AMD's K8 and K10 microcode updates are encoded (but not encrypted or signed)
in a proprietary format which is only partly explained in the paper. The update
process decodes the blob, which includes sets of microcode instructions
(microinstructions) called `triads`, and values for `match registers` which are
microcode-internal register-like locations that hold addresses of triads in
microcode ROM. The new triads that the update carries are mapped in
microcode RAM directly after the address space of the ROM, and the match
register values are copied to their respective match registers. The match
registers (which are eight by design) can be used to run the updated
microcode triads by redirecting execution to the new addresses in RAM. The
authors use this to hook CPU microcode triads and run their version of the
div instruction for example. One limitation (apart from the only eight
available match registers) is that instructions are separated into
performance critical ones (called direct path instructions), and more complex
ones (called vector path instructions). Match registers are used only for the
latter. Since the microcode update is mapped into RAM, it's not permanent,
but is applied at each boot.

Using the above way to load arbitrary microcode triads via updates, the
authors then proceeded to reverse the microcode instruction set by trial and
error using a minimal operating system they developed. With some information
from AMD's patents and bruteforcing the microcode instruction fields, they
observed the protection faults and CPU states their triads caused. This led
to around 40% disassembling of existing microcode updates, which is an
impressive feat.

The paper's <a href="https://github.com/RUB-SysSec/Microcode">accompanying code</a>
includes <a href="https://github.com/RUB-SysSec/Microcode/tree/master/updatedriver">a
patch for the Linux kernel</a> that applies a microcode update from file
`/lib/firmware/amd-ucode/myupdate.bin` without any checks. It also includes
<a href="https://github.com/RUB-SysSec/Microcode/tree/master/updates">various
sample updates</a> (in binary and encoded format, and microinstruction source)
implementing instrumentation and backdoor PoCs described in the paper.

The references seem complete, apart from neglecting to cite Ben Hawkes'
<a href="http://inertiawar.com/microcode/">notes on Intel microcode updates</a>.
