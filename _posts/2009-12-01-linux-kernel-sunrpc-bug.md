---
title: "Advisory: Linux kernel SUNRPC off-by-two buffer overflow"
layout: post
tags:
  - exploitation
  - advisories
  - census
  - kernel
  - linux
  - security
  - sunrpc
---

*Note: The original advisory can be found
[here](http://census-labs.com/news/2009/12/01/linux-kernel-sunrpc/).*

CENSUS ID:         | CENSUS-2009-0005
Affected products: | Linux kernel versions from 2.6.32 to 2.6.32-rc7
Class:             | Off-by-two stack buffer overflow
Discovered by:     | Patroklos Argyroudis

We have found an off-by-two stack buffer overflow in the Linux kernel SUNRPC 
implementation. Linux kernel versions from 2.6.32 to 2.6.32-rc7 are affected.

### Details

There is an off-by-two stack buffer overflow in function `rpc_uaddr2sockaddr()` 
of file `net/sunrpc/addr.c` in the Linux kernel SUNRPC implementation. It was 
introduced in commit
[a02d692611348f11ee1bc37431a883c3ff2de23e](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=commit;h=a02d692611348f11ee1bc37431a883c3ff2de23e).

The function `rpc_uaddr2sockaddr()` that is used to convert a universal address 
to a socket address takes as an argument the `size_t` variable `uaddr_len` (the 
length of the universal address string). The stack buffer `buf` is declared in 
line 315 to be of size `RPCBIND_MAXUADDRLEN`. If the passed argument 
`uaddr_len` is equal to `RPCBIND_MAXUADDRLEN` then the condition of line 319 is 
false and then at lines 324 and 325 there are two out-of-bounds assignments:

{% highlight c %}
312: size_t rpc_uaddr2sockaddr(const char *uaddr, const size_t uaddr_len,
313:                           struct sockaddr *sap, const size_t salen)
314: {
315:        char *c, buf[RPCBIND_MAXUADDRLEN];
            ...
319:        if (uaddr_len > sizeof(buf))
320:            return 0;
            ...
324:        buf[uaddr_len] = '\n';
325:        buf[uaddr_len + 1] = '\0';
            ...
363: }
364: EXPORT_SYMBOL_GPL(rpc_uaddr2sockaddr);
{% endhighlight %}

Since the function `rpc_uaddr2sockaddr()` is declared as an `EXPORT_SYMBOL_GPL` 
function it can be used by kernel modules and potentially be reachable by user 
input. The bug was [reported](http://bugzilla.kernel.org/show_bug.cgi?id=14546)
and fixed in
[2.6.32-rc8](http://www.kernel.org/pub/linux/kernel/v2.6/testing/ChangeLog-2.6.32-rc8)
(commit
[1e360a60b24ad8f8685af66fa6de10ce46693a4b](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=commit;h=1e360a60b24ad8f8685af66fa6de10ce46693a4b)).
