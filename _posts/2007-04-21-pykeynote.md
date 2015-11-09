---
id: 9
title: pykeynote
author: argp
layout: post
guid: http://argp.gr/blog/?p=9
permalink: /2007/04/21/pykeynote/
categories:
  - code
tags:
  - authorization
  - code
  - keynote
  - python
  - trust management
---
My latest coding project is [pykeynote][1]; a Python extension module for KeyNote. It provides a high-level, object-oriented interface to the [KeyNote trust management API][2]. From the KeyNote web page:

> Trust management is a unified approach to specifying and interpreting security policies, credentials, and relationships; it allows direct authorization of security-critical actions. KeyNote credentials describe a specific delegation of trust and subsume the role of public key certificates; unlike traditional certificates, which bind keys to names, credentials can bind keys directly to the authorization to perform specific tasks.

For more information on KeyNote see [RFC 2704][3], [keynote(1)][4], [keynote(3)][5], [keynote(4)][6] and [keynote(5)][7]. Also, a nice introductory article can be found [here][8].

Although I have developed [pykeynote][1] on Linux, and minimally tested it on OpenBSD, it will probably work on all Unix-like systems that satisfy the following requirements:

  * Python version 2.3 or higher. 
      * [Pyrex][9] version 0.9.4 or higher (optional). 
          * The [KeyNote trust management system][2] (tested with version 2.3). 
              * The [OpenSSL cryptographic toolkit][10] (tested with version 0.9.8d). </ul> 
                For the details you can browse the [SVN repository][11]; I have included a comprehensive testsuite and a sample application. There is also the [epydoc generated API documentation][12] to help you start coding.

 [1]: http://code.google.com/p/pykeynote/
 [2]: http://www1.cs.columbia.edu/~angelos/keynote.html
 [3]: http://www.apps.ietf.org/rfc/rfc2704.html
 [4]: http://www.openbsd.org/cgi-bin/<br />
man.cgi?query=keynote&#038;sektion=1&#038;arch=i386&#038;apropos=0&#038;manpath=OpenBSD+Current
 [5]: http://www.openbsd.org/cgi-bin/<br />
man.cgi?query=keynote&#038;sektion=3&#038;arch=i386&#038;apropos=0&#038;manpath=OpenBSD+Current
 [6]: http://www.openbsd.org/cgi-bin/<br />
man.cgi?query=keynote&#038;sektion=4&#038;arch=i386&#038;apropos=0&#038;manpath=OpenBSD+Current
 [7]: http://www.openbsd.org/cgi-bin/man.cgi?query=keynote&#038;sektion=5&#038;arch=i386&#038;apropos=0&#038;manpath=OpenBSD+Current
 [8]: http://www.crypto.com/trustmgt/kn.html
 [9]: http://www.cosc.canterbury.ac.nz/~greg/python/Pyrex/
 [10]: http://www.openssl.org/
 [11]: http://pykeynote.googlecode.com/svn/
 [12]: http://ntrg.cs.tcd.ie/~argp/software/pykeynote-1.0-doc/