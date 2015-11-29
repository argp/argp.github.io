---
title: FreeBSD kernel debugging
layout: post
tags:
  - ddb
  - debugging
  - freebsd
  - gdb
  - kernel
  - vmware
---
The FreeBSD kernel can be debugged with the
[ddb(4)](http://www.freebsd.org/cgi/man.cgi?query=ddb&sektion=4&apropos=0&manpath=FreeBSD+7.1-RELEASE)
interactive kernel debugger. Although the latest production release of FreeBSD
([7.1](http://www.freebsd.org/releases/7.1R/announce.html) at the time of this
writing) adds some [very useful
features](http://www.freebsd.org/cgi/man.cgi?query=ddb&apropos=0&sektion=0&manpath=FreeBSD+7.1-RELEASE),
ddb is still lacking the flexibility of [gdb](http://www.gnu.org/software/gdb/).

The FreeBSD developer's handbook has a section on [kernel debugging using remote
gdb](http://www.freebsd.org/doc/en_US.ISO8859-1/books/developers-handbook/kerne%20ldebug-online-gdb.html), 
but it is not directly applicable to VMware-based installations. The solution 
is to use VMware's feature of creating virtual serial ports as named 
pipes to emulate a serial connection between two FreeBSD virtual machines.

The first FreeBSD virtual machine, let's call it the target host to 
follow the handbook's terminology, is the machine that the experimental 
kernel code runs on. The second, the debugging host, is the one that will run 
gdb and connect over the virtual serial connection to the target host. The 
target host's kernel needs to be compiled with the following options:

{% highlight bash %}
makeoptions DEBUG=-g
options GDB
options DDB
options KDB
{% endhighlight %}

Furthermore, the serial port needs to be defined in the device flags in the 
`/boot/device.hints` file of the target host by setting the `0x80` bit, and the 
`0x10` bit for specifying that the kernel gdb backend is to be accessed via 
remote debugging over this port:

{% highlight bash %}
hint.sio.0.flags="0x90"
{% endhighlight %}

Also, edit the target host's `/etc/sysctl.conf` file to include the 
following self-explanatory kernel parameters:

{% highlight bash %}
debug.kdb.current=ddb
debug.debugger_on_panic=1
{% endhighlight %}

After the compilation and installation of the new kernel on the target host, 
the `/usr/obj/usr/src/sys/TARGET_HOST` directory (assuming you have named the 
new kernel `TARGET_HOST`) needs to be copied to the debugging host (for example 
with `scp -r`).

For the following steps both virtual machines need to be turned off. In VMware 
go to the tab of the target host, click *Edit virtual machine 
settings*->*Add*->*Serial Port*->*Output to named pipe*. Enter `/tmp/com_1` (or 
whatever you want) as the named pipe, select *This end is the server* and *The 
other end is a virtual machine*. Then perform the same steps on the debugging 
host's virtual machine, enter the same named pipe, but select *This end 
is the client* in this case. The `/tmp/com_1` named pipe on the machine that 
runs VMware (Linux in our case) will be used as a virtual serial connection 
between the two FreeBSD guests.

Now power on the target host normally, cause a kernel panic or start the kernel 
debugger manually, and type `gdb` and then `s`:

{% highlight bash %}
[root@target_host]# sysctl debug.kdb.enter=1
KDB: enter: sysctl debug.kdb.enter
[thread pid 578 tid 100063 ]
Stopped at kdb_enter+0x2b: nop
db> gdb
Step to enter the remote GDB backend.
db> s
{% endhighlight %}

On the debugging host you need to find the device that corresponds to the 
virtual serial port you defined in VMware. On our setup it is `/dev/cuad0`. 
Then start a `kgdb` remote debugging session in the 
`/usr/obj/usr/src/sys/TARGET_HOST` directory, passing as arguments the serial 
port device and the kernel to be debugged:

{% highlight bash %}
[root@debugging_host ~]# cd /usr/obj/usr/src/sys/TARGET_HOST
[root@debugging_host /usr/obj/usr/src/sys/TARGET_HOST]# kgdb -r /dev/cuad0 ./kernel.debug
GNU gdb 6.1.1 [FreeBSD]
Copyright 2004 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License, and you are
welcome to change it and/or distribute copies of it under certain conditions.
Type "show copying" to see the conditions.
There is absolutely no warranty for GDB.  Type "show warranty" for details.
This GDB was configured as "i386-marcel-freebsd".
Switching to remote protocol
kdb_enter (msg=0x23 <Address 0x23 out of bounds>) at /usr/src/sys/kern/subr_kdb.c:270
 
Unread portion of the kernel message buffer:
KDB: enter: sysctl debug.kdb.enter
 
#0  kdb_enter (msg=0x23 <Address 0x23 out of bounds>) at /usr/src/sys/kern/subr_kdb.c:270
(kgdb) bt
#0  kdb_enter (msg=0x23 <Address 0x23 out of bounds>) at /usr/src/sys/kern/subr_kdb.c:270
#1  0xc0657710 in kdb_sysctl_enter (oidp=0xc08d3fa0, arg1=0x0, arg2=0, req=0xcca54c04) at
 /usr/src/sys/kern/subr_kdb.c:175
#2  0xc0646f2b in sysctl_root (oidp=0x0, arg1=0x0, arg2=0, req=0xcca54c04) at
 /usr/src/sys/kern/kern_sysctl.c:1248
#3  0xc0647128 in userland_sysctl (td=0x23, name=0xcca54c74, namelen=3,
 old=0xcca54c04, oldlenp=0x0, inkernel=, new=0xbfbfe428, newlen=35,
 retval=0xcca54c70, flags=35) at /usr/src/sys/kern/kern_sysctl.c:1347
#4  0xc0646fcb in __sysctl (td=0xc164d180, uap=0xcca54d04) at
 /usr/src/sys/kern/kern_sysctl.c:1282
#5  0xc0811dcf in syscall (frame=
 {tf_fs = 59, tf_es = 59, tf_ds = 59, tf_edi = 3, tf_esi = ,
 tf_ebp = -1077943368, tf_isp = -861581980, tf_ebx = 672367844,
 tf_edx = , tf_ecx = -1077941184, tf_eax = 202, tf_trapno = 12,
 tf_err = 2, tf_eip = 671840819, tf_cs = 51, tf_eflags = 658,
 tf_esp = -1077943428, tf_ss = 59}) at
 /usr/src/sys/i386/i386/trap.c:976
#6  0xc08007bf in Xint0x80_syscall () at
 /usr/src/sys/i386/i386/exception.s:200
#7  0x00000033 in ?? ()
Previous frame inner to this frame (corrupt stack?)
(kgdb)
{% endhighlight %}

That's it. Now let's do some kernel debugging.
