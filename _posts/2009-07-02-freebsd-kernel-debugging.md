---
id: 102
title: FreeBSD kernel debugging
author: argp
layout: post
guid: http://argp.gr/blog/?p=102
permalink: /2009/07/02/freebsd-kernel-debugging/
aktt_notify_twitter:
  - no
categories:
  - freebsd
  - kernel
tags:
  - ddb
  - debugging
  - freebsd
  - gdb
  - kernel
  - vmware
---
The FreeBSD kernel can be debugged with the <a href="http://www.freebsd.org/cgi/man.cgi?query=ddb&#038;sektion=4&#038;apropos=0&#038;manpath=FreeBSD+7.1-RELEASE" target="blank">ddb(4)</a> interactive kernel debugger. Although the latest production release of FreeBSD (<a href="http://www.freebsd.org/releases/7.1R/announce.html" target="blank">7.1</a> at the time of this writing) adds some <a href="http://www.freebsd.org/cgi/man.cgi?query=ddb&#038;apropos=0&#038;sektion=0&#038;manpath=FreeBSD+7.1-RELEASE" target="blank">very useful features</a>, ddb is still lacking the flexibility of <a href="http://www.gnu.org/software/gdb/" target="blank">gdb</a>.

The FreeBSD developer&#8217;s handbook has a section on <a href="http://www.freebsd.org/doc/en_US.ISO8859-1/books/developers-handbook/kerneldebug-online-gdb.html" target="blank">kernel debugging using remote gdb</a>, but it is not directly applicable to VMware-based installations. The solution is to use VMware&#8217;s feature of creating virtual serial ports as named pipes to emulate a serial connection between two FreeBSD virtual machines.

The first FreeBSD virtual machine, let&#8217;s call it the target host to follow the handbook&#8217;s terminology, is the machine that the experimental kernel code runs on. The second, the debugging host, is the one that will run gdb and connect over the virtual serial connection to the target host. The target host&#8217;s kernel needs to be compiled with the following options:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="bash" style="font-family:monospace;">makeoptions <span style="color: #007800;">DEBUG</span>=-g
options GDB
options DDB
options KDB</pre>
      </td>
    </tr>
  </table>
</div>

Furthermore, the serial port needs to be defined in the device flags in the `/boot/device.hints` file of the target host by setting the `0x80` bit, and the `0x10` bit for specifying that the kernel gdb backend is to be accessed via remote debugging over this port:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="bash" style="font-family:monospace;">hint.sio.0.flags=<span style="color: #ff0000;">"0x90"</span></pre>
      </td>
    </tr>
  </table>
</div>

Also, edit the target host&#8217;s `/etc/sysctl.conf` file to include the following self-explanatory kernel parameters:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="bash" style="font-family:monospace;">debug.kdb.current=ddb
debug.debugger_on_panic=<span style="color: #000000;">1</span></pre>
      </td>
    </tr>
  </table>
</div>

After the compilation and installation of the new kernel on the target host, the `/usr/obj/usr/src/sys/TARGET_HOST` directory (assuming you have named the new kernel `TARGET_HOST`) needs to be copied to the debugging host (for example with `scp -r`).

For the following steps both virtual machines need to be turned off. In VMware go to the tab of the target host, click *Edit virtual machine settings*->*Add*->*Serial Port*->*Output to named pipe*. Enter `/tmp/com_1` (or whatever you want) as the named pipe, select *This end is the server* and *The other end is a virtual machine*. Then perform the same steps on the debugging host&#8217;s virtual machine, enter the same named pipe, but select *This end is the client* in this case. The `/tmp/com_1` named pipe on the machine that runs VMware (Linux in our case) will be used as a virtual serial connection between the two FreeBSD guests.

Now power on the target host normally, cause a kernel panic or start the kernel debugger manually, and type `gdb` and then `s`:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">&#91;</span>root<span style="color: #000000; font-weight: bold;">@</span>target_host<span style="color: #7a0874; font-weight: bold;">&#93;</span><span style="color: #666666; font-style: italic;"># sysctl debug.kdb.enter=1</span>
KDB: enter: sysctl debug.kdb.enter
<span style="color: #7a0874; font-weight: bold;">&#91;</span>thread pid <span style="color: #000000;">578</span> tid <span style="color: #000000;">100063</span> <span style="color: #7a0874; font-weight: bold;">&#93;</span>
Stopped at kdb_enter+0x2b: <span style="color: #c20cb9; font-weight: bold;">nop</span>
db<span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #c20cb9; font-weight: bold;">gdb</span>
Step to enter the remote GDB backend.
db<span style="color: #000000; font-weight: bold;">&gt;</span> s</pre>
      </td>
    </tr>
  </table>
</div>

On the debugging host you need to find the device that corresponds to the virtual serial port you defined in VMware. On our setup it is `/dev/cuad0`. Then start a `kgdb` remote debugging session in the `/usr/obj/usr/src/sys/TARGET_HOST` directory, passing as arguments the serial port device and the kernel to be debugged:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">&#91;</span>root<span style="color: #000000; font-weight: bold;">@</span>debugging_host ~<span style="color: #7a0874; font-weight: bold;">&#93;</span><span style="color: #666666; font-style: italic;"># cd /usr/obj/usr/src/sys/TARGET_HOST</span>
<span style="color: #7a0874; font-weight: bold;">&#91;</span>root<span style="color: #000000; font-weight: bold;">@</span>debugging_host <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>obj<span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>src<span style="color: #000000; font-weight: bold;">/</span>sys<span style="color: #000000; font-weight: bold;">/</span>TARGET_HOST<span style="color: #7a0874; font-weight: bold;">&#93;</span><span style="color: #666666; font-style: italic;"># kgdb -r /dev/cuad0 \</span>
  .<span style="color: #000000; font-weight: bold;">/</span>kernel.debug
GNU <span style="color: #c20cb9; font-weight: bold;">gdb</span> 6.1.1 <span style="color: #7a0874; font-weight: bold;">&#91;</span>FreeBSD<span style="color: #7a0874; font-weight: bold;">&#93;</span>
Copyright <span style="color: #000000;">2004</span> Free Software Foundation, Inc.
GDB is <span style="color: #c20cb9; font-weight: bold;">free</span> software, covered by the GNU General Public License, and you are
welcome to change it and<span style="color: #000000; font-weight: bold;">/</span>or distribute copies of it under certain conditions.
Type <span style="color: #ff0000;">"show copying"</span> to see the conditions.
There is absolutely no warranty <span style="color: #000000; font-weight: bold;">for</span> GDB.  Type <span style="color: #ff0000;">"show warranty"</span> <span style="color: #000000; font-weight: bold;">for</span> details.
This GDB was configured <span style="color: #c20cb9; font-weight: bold;">as</span> <span style="color: #ff0000;">"i386-marcel-freebsd"</span>.
Switching to remote protocol
kdb_enter <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">msg</span>=0x23 <span style="color: #000000; font-weight: bold;">&lt;</span>Address 0x23 out of bounds<span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> at
 <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>src<span style="color: #000000; font-weight: bold;">/</span>sys<span style="color: #000000; font-weight: bold;">/</span>kern<span style="color: #000000; font-weight: bold;">/</span>subr_kdb.c:<span style="color: #000000;">270</span>
<span style="color: #000000;">270</span> <span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
Unread portion of the kernel message buffer:
KDB: enter: sysctl debug.kdb.enter
&nbsp;
<span style="color: #666666; font-style: italic;">#0  kdb_enter (msg=0x23 &lt;Address 0x23 out of bounds&gt;) at</span>
 <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>src<span style="color: #000000; font-weight: bold;">/</span>sys<span style="color: #000000; font-weight: bold;">/</span>kern<span style="color: #000000; font-weight: bold;">/</span>subr_kdb.c:<span style="color: #000000;">270</span>
<span style="color: #000000;">270</span> <span style="color: #7a0874; font-weight: bold;">&#125;</span>
<span style="color: #7a0874; font-weight: bold;">&#40;</span>kgdb<span style="color: #7a0874; font-weight: bold;">&#41;</span> bt
<span style="color: #666666; font-style: italic;">#0  kdb_enter (msg=0x23 &lt;Address 0x23 out of bounds&gt;) at</span>
 <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>src<span style="color: #000000; font-weight: bold;">/</span>sys<span style="color: #000000; font-weight: bold;">/</span>kern<span style="color: #000000; font-weight: bold;">/</span>subr_kdb.c:<span style="color: #000000;">270</span>
<span style="color: #666666; font-style: italic;">#1  0xc0657710 in kdb_sysctl_enter (oidp=0xc08d3fa0, arg1=0x0, arg2=0,</span>
 <span style="color: #007800;">req</span>=0xcca54c04<span style="color: #7a0874; font-weight: bold;">&#41;</span> at <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>src<span style="color: #000000; font-weight: bold;">/</span>sys<span style="color: #000000; font-weight: bold;">/</span>kern<span style="color: #000000; font-weight: bold;">/</span>subr_kdb.c:<span style="color: #000000;">175</span>
<span style="color: #666666; font-style: italic;">#2  0xc0646f2b in sysctl_root (oidp=0x0, arg1=0x0, arg2=0, req=0xcca54c04) at</span>
 <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>src<span style="color: #000000; font-weight: bold;">/</span>sys<span style="color: #000000; font-weight: bold;">/</span>kern<span style="color: #000000; font-weight: bold;">/</span>kern_sysctl.c:<span style="color: #000000;">1248</span>
<span style="color: #666666; font-style: italic;">#3  0xc0647128 in userland_sysctl (td=0x23, name=0xcca54c74, namelen=3,</span>
 <span style="color: #007800;">old</span>=0xcca54c04, <span style="color: #007800;">oldlenp</span>=0x0, <span style="color: #007800;">inkernel</span>=<span style="color: #000000;"></span>, <span style="color: #007800;">new</span>=0xbfbfe428, <span style="color: #007800;">newlen</span>=<span style="color: #000000;">35</span>,
 <span style="color: #007800;">retval</span>=0xcca54c70, <span style="color: #007800;">flags</span>=<span style="color: #000000;">35</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> at <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>src<span style="color: #000000; font-weight: bold;">/</span>sys<span style="color: #000000; font-weight: bold;">/</span>kern<span style="color: #000000; font-weight: bold;">/</span>kern_sysctl.c:<span style="color: #000000;">1347</span>
<span style="color: #666666; font-style: italic;">#4  0xc0646fcb in __sysctl (td=0xc164d180, uap=0xcca54d04) at</span>
 <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>src<span style="color: #000000; font-weight: bold;">/</span>sys<span style="color: #000000; font-weight: bold;">/</span>kern<span style="color: #000000; font-weight: bold;">/</span>kern_sysctl.c:<span style="color: #000000;">1282</span>
<span style="color: #666666; font-style: italic;">#5  0xc0811dcf in syscall (frame=</span>
 <span style="color: #7a0874; font-weight: bold;">&#123;</span>tf_fs = <span style="color: #000000;">59</span>, tf_es = <span style="color: #000000;">59</span>, tf_ds = <span style="color: #000000;">59</span>, tf_edi = <span style="color: #000000;">3</span>, tf_esi = <span style="color: #000000;"></span>,
 tf_ebp = -<span style="color: #000000;">1077943368</span>, tf_isp = -<span style="color: #000000;">861581980</span>, tf_ebx = <span style="color: #000000;">672367844</span>,
 tf_edx = <span style="color: #000000;"></span>, tf_ecx = -<span style="color: #000000;">1077941184</span>, tf_eax = <span style="color: #000000;">202</span>, tf_trapno = <span style="color: #000000;">12</span>,
 tf_err = <span style="color: #000000;">2</span>, tf_eip = <span style="color: #000000;">671840819</span>, tf_cs = <span style="color: #000000;">51</span>, tf_eflags = <span style="color: #000000;">658</span>,
 tf_esp = -<span style="color: #000000;">1077943428</span>, tf_ss = <span style="color: #000000;">59</span><span style="color: #7a0874; font-weight: bold;">&#125;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> at
 <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>src<span style="color: #000000; font-weight: bold;">/</span>sys<span style="color: #000000; font-weight: bold;">/</span>i386<span style="color: #000000; font-weight: bold;">/</span>i386<span style="color: #000000; font-weight: bold;">/</span>trap.c:<span style="color: #000000;">976</span>
<span style="color: #666666; font-style: italic;">#6  0xc08007bf in Xint0x80_syscall () at</span>
 <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>src<span style="color: #000000; font-weight: bold;">/</span>sys<span style="color: #000000; font-weight: bold;">/</span>i386<span style="color: #000000; font-weight: bold;">/</span>i386<span style="color: #000000; font-weight: bold;">/</span>exception.s:<span style="color: #000000;">200</span>
<span style="color: #666666; font-style: italic;">#7  0x00000033 in ?? ()</span>
Previous frame inner to this frame <span style="color: #7a0874; font-weight: bold;">&#40;</span>corrupt stack?<span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#40;</span>kgdb<span style="color: #7a0874; font-weight: bold;">&#41;</span></pre>
      </td>
    </tr>
  </table>
</div>

That&#8217;s it. Now let&#8217;s do some debugging.