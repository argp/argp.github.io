---
id: 256
title: FreeBSD kernel NFS client local vulnerabilities
author: argp
layout: post
guid: http://argp.gr/blog/?p=256
permalink: /2010/05/23/freebsd-kernel-nfsclient/
aktt_notify_twitter:
  - no
categories:
  - advisories
  - exploitation
  - freebsd
  - kernel
  - research
  - security
tags:
  - advisories
  - census
  - freebsd
  - kernel
  - nfsclient
  - research
  - security
---
<table>
  <tr>
    <td>
      census ID:
    </td>
    
    <td>
      census-2010-0001
    </td>
  </tr>
  
  <tr>
    <td>
      CVE ID:
    </td>
    
    <td>
      <a href="http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2010-2020">CVE-2010-2020</a>
    </td>
  </tr>
  
  <tr>
    <td>
      Affected Products:
    </td>
    
    <td>
      FreeBSD 8.0-RELEASE, 7.3-RELEASE, 7.2-RELEASE
    </td>
  </tr>
  
  <tr>
    <td>
      Class:
    </td>
    
    <td>
      Improper Input Validation (<a href="http://cwe.mitre.org/data/definitions/20.html">CWE-20</a>)
    </td>
  </tr>
  
  <tr>
    <td>
      Remote:
    </td>
    
    <td>
      No
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

We have discovered two improper input validation vulnerabilities in the FreeBSD kernel&#8217;s NFS client-side implementation (FreeBSD 8.0-RELEASE, 7.3-RELEASE and 7.2-RELEASE) that allow local unprivileged users to escalate their privileges, or to crash the system by performing a denial of service attack.

### Details

[FreeBSD][1] is an advanced operating system which focuses on reliability and performance. More information about its features can be found [here][2].

FreeBSD 8.0-RELEASE, 7.3-RELEASE and 7.2-RELEASE employ an improper input validation method in the kernel&#8217;s NFS client-side implementation. Specifically, the first vulnerability is in function `nfs_mount()` (file `src/sys/nfsclient/nfs_vfsops.c`) which is reachable from the `mount(2)` and `nmount(2)` system calls. In order for them to be enabled for unprivileged users the `sysctl(8)` variable `vfs.usermount` must be set to a non-zero value.

The function `nfs_mount()` employs an insufficient input validation method for copying data passed in a structure of type `nfs_args` from userspace to kernel. Specifically, the file handle buffer to be mounted (`args.fh`) and its size (`args.fhsize`) are completely user-controllable. The unbounded copy operation is in file `src/sys/nfsclient/nfs_vfsops.c` (the excerpts are from 8.0-RELEASE):

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1094
1095
1096
1097
1098
1099
</pre>
      </td>
      
      <td class="code">
        <pre class="c" style="font-family:monospace;"><span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>has_fh_opt<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
      error <span style="color: #339933;">=</span> copyin<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>caddr_t<span style="color: #009900;">&#41;</span>args.<span style="color: #202020;">fh</span><span style="color: #339933;">,</span> <span style="color: #009900;">&#40;</span>caddr_t<span style="color: #009900;">&#41;</span>nfh<span style="color: #339933;">,</span>
           args.<span style="color: #202020;">fhsize</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span>error<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
         <span style="color: #b1b100;">goto</span> out<span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre>
      </td>
    </tr>
  </table>
</div>

The declaration of the variables `args` and `nfh` is at:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>786
787
788
789
790
791
792
793
794
795
796
797
798
799
800
801
802
803
804
805
806
807
808
809
810
811
812
813
814
815
816
817
818
819
820
</pre>
      </td>
      
      <td class="code">
        <pre class="c" style="font-family:monospace;"><span style="color: #993333;">static</span> <span style="color: #993333;">int</span>
nfs_mount<span style="color: #009900;">&#40;</span><span style="color: #993333;">struct</span> mount <span style="color: #339933;">*</span>mp<span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
        <span style="color: #993333;">struct</span> nfs_args args <span style="color: #339933;">=</span> <span style="color: #009900;">&#123;</span>
            .<span style="color: #202020;">version</span> <span style="color: #339933;">=</span> NFS_ARGSVERSION<span style="color: #339933;">,</span>
            .<span style="color: #202020;">addr</span> <span style="color: #339933;">=</span> NULL<span style="color: #339933;">,</span>
            .<span style="color: #202020;">addrlen</span> <span style="color: #339933;">=</span> <span style="color: #993333;">sizeof</span> <span style="color: #009900;">&#40;</span><span style="color: #993333;">struct</span> sockaddr_in<span style="color: #009900;">&#41;</span><span style="color: #339933;">,</span>
            .<span style="color: #202020;">sotype</span> <span style="color: #339933;">=</span> SOCK_STREAM<span style="color: #339933;">,</span>
            .<span style="color: #202020;">proto</span> <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">,</span>
            .<span style="color: #202020;">fh</span> <span style="color: #339933;">=</span> NULL<span style="color: #339933;">,</span>
            .<span style="color: #202020;">fhsize</span> <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">,</span>
            .<span style="color: #202020;">flags</span> <span style="color: #339933;">=</span> NFSMNT_RESVPORT<span style="color: #339933;">,</span>
            .<span style="color: #202020;">wsize</span> <span style="color: #339933;">=</span> NFS_WSIZE<span style="color: #339933;">,</span>
            .<span style="color: #202020;">rsize</span> <span style="color: #339933;">=</span> NFS_RSIZE<span style="color: #339933;">,</span>
            .<span style="color: #202020;">readdirsize</span> <span style="color: #339933;">=</span> NFS_READDIRSIZE<span style="color: #339933;">,</span>
            .<span style="color: #202020;">timeo</span> <span style="color: #339933;">=</span> <span style="color: #0000dd;">10</span><span style="color: #339933;">,</span>
            .<span style="color: #202020;">retrans</span> <span style="color: #339933;">=</span> NFS_RETRANS<span style="color: #339933;">,</span>
            .<span style="color: #202020;">maxgrouplist</span> <span style="color: #339933;">=</span> NFS_MAXGRPS<span style="color: #339933;">,</span>
            .<span style="color: #202020;">readahead</span> <span style="color: #339933;">=</span> NFS_DEFRAHEAD<span style="color: #339933;">,</span>
            .<span style="color: #202020;">wcommitsize</span> <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">,</span>                   <span style="color: #808080; font-style: italic;">/* was: NQ_DEFLEASE */</span>
            .<span style="color: #202020;">deadthresh</span> <span style="color: #339933;">=</span> NFS_MAXDEADTHRESH<span style="color: #339933;">,</span>    <span style="color: #808080; font-style: italic;">/* was: NQ_DEADTHRESH */</span>
            .<span style="color: #202020;">hostname</span> <span style="color: #339933;">=</span> NULL<span style="color: #339933;">,</span>
            <span style="color: #808080; font-style: italic;">/* args version 4 */</span>
            .<span style="color: #202020;">acregmin</span> <span style="color: #339933;">=</span> NFS_MINATTRTIMO<span style="color: #339933;">,</span>
            .<span style="color: #202020;">acregmax</span> <span style="color: #339933;">=</span> NFS_MAXATTRTIMO<span style="color: #339933;">,</span>
            .<span style="color: #202020;">acdirmin</span> <span style="color: #339933;">=</span> NFS_MINDIRATTRTIMO<span style="color: #339933;">,</span>
            .<span style="color: #202020;">acdirmax</span> <span style="color: #339933;">=</span> NFS_MAXDIRATTRTIMO<span style="color: #339933;">,</span>
        <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
        <span style="color: #993333;">int</span> error<span style="color: #339933;">,</span> ret<span style="color: #339933;">,</span> has_nfs_args_opt<span style="color: #339933;">;</span>
        <span style="color: #993333;">int</span> has_addr_opt<span style="color: #339933;">,</span> has_fh_opt<span style="color: #339933;">,</span> has_hostname_opt<span style="color: #339933;">;</span>
        <span style="color: #993333;">struct</span> sockaddr <span style="color: #339933;">*</span>nam<span style="color: #339933;">;</span>
        <span style="color: #993333;">struct</span> vnode <span style="color: #339933;">*</span>vp<span style="color: #339933;">;</span>
        <span style="color: #993333;">char</span> hst<span style="color: #009900;">&#91;</span>MNAMELEN<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
        <span style="color: #993333;">size_t</span> len<span style="color: #339933;">;</span>
        u_char nfh<span style="color: #009900;">&#91;</span>NFSX_V3FHMAX<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span></pre>
      </td>
    </tr>
  </table>
</div>

This vulnerability can cause a kernel stack overflow which leads to privilege escalation on FreeBSD 7.3-RELEASE and 7.2-RELEASE. On FreeBSD 8.0-RELEASE the result is a kernel crash/denial of service due to the SSP/ProPolice kernel stack-smashing protection which is enabled by default. Versions 7.1-RELEASE and earlier do not appear to be vulnerable since the bug was introduced in 7.2-RELEASE. In order to demonstrate the impact of the vulnerability we have developed a [proof-of-concept privilege escalation exploit][3]. A sample run of the exploit follows:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">&#91;</span>argp<span style="color: #000000; font-weight: bold;">@</span>julius ~<span style="color: #7a0874; font-weight: bold;">&#93;</span>$ <span style="color: #c20cb9; font-weight: bold;">uname</span> <span style="color: #660033;">-rsi</span>
FreeBSD <span style="color: #000000;">7.3</span>-RELEASE GENERIC
<span style="color: #7a0874; font-weight: bold;">&#91;</span>argp<span style="color: #000000; font-weight: bold;">@</span>julius ~<span style="color: #7a0874; font-weight: bold;">&#93;</span>$ sysctl vfs.usermount
vfs.usermount: <span style="color: #000000;">1</span>
<span style="color: #7a0874; font-weight: bold;">&#91;</span>argp<span style="color: #000000; font-weight: bold;">@</span>julius ~<span style="color: #7a0874; font-weight: bold;">&#93;</span>$ <span style="color: #c20cb9; font-weight: bold;">id</span>
<span style="color: #007800;">uid</span>=<span style="color: #000000;">1001</span><span style="color: #7a0874; font-weight: bold;">&#40;</span>argp<span style="color: #7a0874; font-weight: bold;">&#41;</span> <span style="color: #007800;">gid</span>=<span style="color: #000000;">1001</span><span style="color: #7a0874; font-weight: bold;">&#40;</span>argp<span style="color: #7a0874; font-weight: bold;">&#41;</span> <span style="color: #007800;">groups</span>=<span style="color: #000000;">1001</span><span style="color: #7a0874; font-weight: bold;">&#40;</span>argp<span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#91;</span>argp<span style="color: #000000; font-weight: bold;">@</span>julius ~<span style="color: #7a0874; font-weight: bold;">&#93;</span>$ <span style="color: #c20cb9; font-weight: bold;">gcc</span> <span style="color: #660033;">-Wall</span> nfs_mount_ex.c <span style="color: #660033;">-o</span> nfs_mount_ex
<span style="color: #7a0874; font-weight: bold;">&#91;</span>argp<span style="color: #000000; font-weight: bold;">@</span>julius ~<span style="color: #7a0874; font-weight: bold;">&#93;</span>$ .<span style="color: #000000; font-weight: bold;">/</span>nfs_mount_ex
<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000; font-weight: bold;">*</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> calling nmount<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000; font-weight: bold;">!</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> nmount error: <span style="color: #660033;">-1030740736</span>
nmount: Unknown error: <span style="color: #660033;">-1030740736</span>
<span style="color: #7a0874; font-weight: bold;">&#91;</span>argp<span style="color: #000000; font-weight: bold;">@</span>julius ~<span style="color: #7a0874; font-weight: bold;">&#93;</span>$ <span style="color: #c20cb9; font-weight: bold;">id</span>
<span style="color: #007800;">uid</span>=<span style="color: #000000;"></span><span style="color: #7a0874; font-weight: bold;">&#40;</span>root<span style="color: #7a0874; font-weight: bold;">&#41;</span> <span style="color: #007800;">gid</span>=<span style="color: #000000;"></span><span style="color: #7a0874; font-weight: bold;">&#40;</span>wheel<span style="color: #7a0874; font-weight: bold;">&#41;</span> <span style="color: #007800;">egid</span>=<span style="color: #000000;">1001</span><span style="color: #7a0874; font-weight: bold;">&#40;</span>argp<span style="color: #7a0874; font-weight: bold;">&#41;</span> <span style="color: #007800;">groups</span>=<span style="color: #000000;">1001</span><span style="color: #7a0874; font-weight: bold;">&#40;</span>argp<span style="color: #7a0874; font-weight: bold;">&#41;</span></pre>
      </td>
    </tr>
  </table>
</div>

The second vulnerability exists in the function `mountnfs()` that is called from function `nfs_mount()`:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1119
1120
</pre>
      </td>
      
      <td class="code">
        <pre class="c" style="font-family:monospace;">error <span style="color: #339933;">=</span> mountnfs<span style="color: #009900;">&#40;</span><span style="color: #339933;">&</span>args<span style="color: #339933;">,</span> mp<span style="color: #339933;">,</span> nam<span style="color: #339933;">,</span> args.<span style="color: #202020;">hostname</span><span style="color: #339933;">,</span> <span style="color: #339933;">&</span>vp<span style="color: #339933;">,</span>
    curthread<span style="color: #339933;">-&gt;</span>td_ucred<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>
      </td>
    </tr>
  </table>
</div>

The function `mountnfs()` is reachable from the `mount(2)` and `nmount(2)` system calls by unprivileged users. As with the `nfs_mount()` case above, this requires the `sysctl(8)` variable `vfs.usermount` to be set to a non-zero value.

The file handle to be mounted (`argp->fh`) and its size (`argp->fhsize`) are passed to function `mountnfs()` from function `nfs_mount()` and are user-controllable. These are subsequently used in an unbounded `bcopy()` call (file `src/sys/nfsclient/nfs_vfsops.c`):

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1219
</pre>
      </td>
      
      <td class="code">
        <pre class="c" style="font-family:monospace;">bcopy<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>caddr_t<span style="color: #009900;">&#41;</span>argp<span style="color: #339933;">-&gt;</span>fh<span style="color: #339933;">,</span> <span style="color: #009900;">&#40;</span>caddr_t<span style="color: #009900;">&#41;</span>nmp<span style="color: #339933;">-&gt;</span>nm_fh<span style="color: #339933;">,</span> argp<span style="color: #339933;">-&gt;</span>fhsize<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>
      </td>
    </tr>
  </table>
</div>

The above can cause a kernel heap overflow when `argp->fh` is bigger than 128 bytes (the size of `nmp->nm_fh`) since `nmp` is an allocated item on the Universal Memory Allocator (UMA, the FreeBSD kernel&#8217;s heap allocator) zone `nfsmount_zone` (again from `src/sys/nfsclient/nfs_vfsops.c`):

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1160
1161
1162
1163
1164
1165
1166
1167
1168
1169
1170
1171
1172
1173
1174
1175
</pre>
      </td>
      
      <td class="code">
        <pre class="c" style="font-family:monospace;"><span style="color: #993333;">static</span> <span style="color: #993333;">int</span>
mountnfs<span style="color: #009900;">&#40;</span><span style="color: #993333;">struct</span> nfs_args <span style="color: #339933;">*</span>argp<span style="color: #339933;">,</span> <span style="color: #993333;">struct</span> mount <span style="color: #339933;">*</span>mp<span style="color: #339933;">,</span> <span style="color: #993333;">struct</span> sockaddr <span style="color: #339933;">*</span>nam<span style="color: #339933;">,</span>
    <span style="color: #993333;">char</span> <span style="color: #339933;">*</span>hst<span style="color: #339933;">,</span> <span style="color: #993333;">struct</span> vnode <span style="color: #339933;">**</span>vpp<span style="color: #339933;">,</span> <span style="color: #993333;">struct</span> ucred <span style="color: #339933;">*</span>cred<span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
        <span style="color: #993333;">struct</span> nfsmount <span style="color: #339933;">*</span>nmp<span style="color: #339933;">;</span>
        <span style="color: #993333;">struct</span> nfsnode <span style="color: #339933;">*</span>np<span style="color: #339933;">;</span>
        <span style="color: #993333;">int</span> error<span style="color: #339933;">;</span>
        <span style="color: #993333;">struct</span> vattr attrs<span style="color: #339933;">;</span>
&nbsp;
        <span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span>mp<span style="color: #339933;">-&gt;</span>mnt_flag <span style="color: #339933;">&</span> MNT_UPDATE<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                nmp <span style="color: #339933;">=</span> VFSTONFS<span style="color: #009900;">&#40;</span>mp<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000066;">printf</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"%s: MNT_UPDATE is no longer handled here<span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">,</span> __func__<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000066;">free</span><span style="color: #009900;">&#40;</span>nam<span style="color: #339933;">,</span> M_SONAME<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #b1b100;">return</span> <span style="color: #009900;">&#40;</span><span style="color: #0000dd;"></span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #b1b100;">else</span> <span style="color: #009900;">&#123;</span>
                nmp <span style="color: #339933;">=</span> uma_zalloc<span style="color: #009900;">&#40;</span>nfsmount_zone<span style="color: #339933;">,</span> M_WAITOK<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>
      </td>
    </tr>
  </table>
</div>

This kernel heap overflow can lead on FreeBSD 8.0-RELEASE, 7.3-RELEASE and 7.2-RELEASE to privilege escalation and/or a kernel crash/denial of service attack. Similarly to the first vulnerability, FreeBSD 7.1-RELEASE and earlier versions do not appear to be vulnerable. We have developed a [proof-of-concept DoS exploit][4] to demonstrate the vulnerability. Furthermore, we have also developed a privilege escalation exploit for this second vulnerability which will not be released at this point.

FreeBSD has released an [official advisory][5] and a [patch][6] to address both vulnerabilities. All affected parties are advised to follow the upgrade instructions included in the advisory and patch their systems.

 [1]: http://www.freebsd.org/
 [2]: http://www.freebsd.org/about.html
 [3]: http://census-labs.com/media/nfs_mount_ex.c
 [4]: http://census-labs.com/media/mountnfsex.c
 [5]: http://security.freebsd.org/advisories/FreeBSD-SA-10:06.nfsclient.asc
 [6]: http://security.FreeBSD.org/patches/SA-10:06/nfsclient.patch