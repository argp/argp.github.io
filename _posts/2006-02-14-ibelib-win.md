---
title: Windows and Windows CE port of the Stanford IBE library
layout: post
tags:
  - code
  - cryptography
  - identity based encryption
  - windows
---
I recently ported the [Stanford IBE library](http://crypto.stanford.edu/ibe/)
to [Windows](https://github.com/argp/ibe-win32) and
[Windows CE](https://github.com/argp/ibe-wince).

My Windows port builds natively using the MSVC++ development tools, while
the one provided at the Stanford IBE page was cross-compiled for Windows
with a Linux port of mingw and only includes the application binaries.

Note: On Windows CE the generation of the
[Solinas prime](https://en.wikipedia.org/wiki/Solinas_prime) in the
function `IBE_setup` (file `ibe_lib.c`) usually takes a couple of seconds.
