---
id: 151
title: Linux kernel SUNRPC off-by-two buffer overflow
author: argp
layout: post
guid: http://argp.gr/blog/?p=151
permalink: /2009/12/01/linux-kernel-sunrpc-bug/
aktt_notify_twitter:
  - no
categories:
  - advisories
  - exploitation
  - kernel
  - linux
  - research
  - security
tags:
  - advisories
  - census
  - kernel
  - linux
  - security
  - sunrpc
---
<table>
  <tr>
    <td>
      census ID:
    </td>
    
    <td>
      census-2009-0005
    </td>
  </tr>
  
  <tr>
    <td>
      Affected Products:
    </td>
    
    <td>
      Linux kernel versions from 2.6.32 to 2.6.32-rc7.
    </td>
  </tr>
  
  <tr>
    <td>
      Class:
    </td>
    
    <td>
      Off-by-two stack buffer overflow.
    </td>
  </tr>
  
  <tr>
    <td>
      Discovered by:
    </td>
    
    <td>
      Patroklos Argyroudis
    </td>
  </tr>
</table>

We have found an off-by-two stack buffer overflow in the Linux kernel SUNRPC implementation. Linux kernel versions from 2.6.32 to 2.6.32-rc7 are affected.

### Details

There is an off-by-two stack buffer overflow in function `rpc_uaddr2sockaddr()` of file `net/sunrpc/addr.c` in the Linux kernel SUNRPC implementation. It was introduced in commit [a02d692611348f11ee1bc37431a883c3ff2de23e][1].

The function `rpc_uaddr2sockaddr()` that is used to convert a universal address to a socket address takes as an argument the `size_t` variable `uaddr_len` (the length of the universal address string). The stack buffer `buf` is declared in line 315 to be of size `RPCBIND_MAXUADDRLEN`. If the passed argument `uaddr_len` is equal to `RPCBIND_MAXUADDRLEN` then the condition of line 319 is false and then at lines 324 and 325 there are two out-of-bounds assignments:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="c" style="font-family:monospace;"><span style="color: #0000dd;">312</span><span style="color: #339933;">:</span> <span style="color: #993333;">size_t</span> rpc_uaddr2sockaddr<span style="color: #009900;">&#40;</span><span style="color: #993333;">const</span> <span style="color: #993333;">char</span> <span style="color: #339933;">*</span>uaddr<span style="color: #339933;">,</span> <span style="color: #993333;">const</span> <span style="color: #993333;">size_t</span> uaddr_len<span style="color: #339933;">,</span>
<span style="color: #0000dd;">313</span><span style="color: #339933;">:</span>                           <span style="color: #993333;">struct</span> sockaddr <span style="color: #339933;">*</span>sap<span style="color: #339933;">,</span> <span style="color: #993333;">const</span> <span style="color: #993333;">size_t</span> salen<span style="color: #009900;">&#41;</span>
<span style="color: #0000dd;">314</span><span style="color: #339933;">:</span> <span style="color: #009900;">&#123;</span>
<span style="color: #0000dd;">315</span><span style="color: #339933;">:</span>        <span style="color: #993333;">char</span> <span style="color: #339933;">*</span>c<span style="color: #339933;">,</span> buf<span style="color: #009900;">&#91;</span>RPCBIND_MAXUADDRLEN<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
            ...
<span style="color: #0000dd;">319</span><span style="color: #339933;">:</span>        <span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span>uaddr_len <span style="color: #339933;">&gt;</span> <span style="color: #993333;">sizeof</span><span style="color: #009900;">&#40;</span>buf<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
<span style="color: #0000dd;">320</span><span style="color: #339933;">:</span>            <span style="color: #b1b100;">return</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
            ...
<span style="color: #0000dd;">324</span><span style="color: #339933;">:</span>        buf<span style="color: #009900;">&#91;</span>uaddr_len<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #ff0000;">'<span style="color: #000099; font-weight: bold;">\n</span>'</span><span style="color: #339933;">;</span>
<span style="color: #0000dd;">325</span><span style="color: #339933;">:</span>        buf<span style="color: #009900;">&#91;</span>uaddr_len <span style="color: #339933;">+</span> <span style="color: #0000dd;">1</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #ff0000;">'<span style="color: #006699; font-weight: bold;">\0</span>'</span><span style="color: #339933;">;</span>
            ...
<span style="color: #0000dd;">363</span><span style="color: #339933;">:</span> <span style="color: #009900;">&#125;</span>
<span style="color: #0000dd;">364</span><span style="color: #339933;">:</span> EXPORT_SYMBOL_GPL<span style="color: #009900;">&#40;</span>rpc_uaddr2sockaddr<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>
      </td>
    </tr>
  </table>
</div>

Since the function `rpc_uaddr2sockaddr()` is declared as an `EXPORT_SYMBOL_GPL` function it can be used by kernel modules and potentially be reachable by user input. The bug was [reported][2] and fixed in [2.6.32-rc8][3] (commit [1e360a60b24ad8f8685af66fa6de10ce46693a4b][4]).

 [1]: http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=commit;h=a02d692611348f11ee1bc37431a883c3ff2de23e
 [2]: http://bugzilla.kernel.org/show_bug.cgi?id=14546
 [3]: http://www.kernel.org/pub/linux/kernel/v2.6/testing/ChangeLog-2.6.32-rc8
 [4]: http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=commit;h=1e360a60b24ad8f8685af66fa6de10ce46693a4b