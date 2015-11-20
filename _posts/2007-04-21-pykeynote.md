---
title: pykeynote
layout: post
tags:
  - authorization
  - code
  - keynote
  - python
  - trust management
---
My latest coding project is [pykeynote](https://github.com/argp/pykeynote);
a Python extension module for KeyNote. It provides a high-level, object-oriented
interface to the [KeyNote trust management
API](http://www1.cs.columbia.edu/~angelos/keynote.html). From the KeyNote web page:

> Trust management is a unified approach to specifying and interpreting security
> policies, credentials, and relationships; it allows direct authorization of
> security-critical actions. KeyNote credentials describe a specific delegation
> of trust and subsume the role of public key certificates; unlike traditional
> certificates, which bind keys to names, credentials can bind keys directly to
> the authorization to perform specific tasks.

For more information on KeyNote see
[RFC 2704](https://tools.ietf.org/html/rfc2704),
[keynote(1)](http://www.openbsd.org/cgi-bin/man.cgi?query=keynote&sektion=1&arch=i386&apropos=0&manpath=OpenBSD+Current),
[keynote(3)](http://www.openbsd.org/cgi-bin/man.cgi?query=keynote&sektion=3&arch=i386&apropos=0&manpath=OpenBSD+Current),
[keynote(4)](http://www.openbsd.org/cgi-bin/man.cgi?query=keynote&sektion=4&arch=i386&apropos=0&manpath=OpenBSD+Current)
and
[keynote(5)](http://www.openbsd.org/cgi-bin/man.cgi?query=keynote&sektion=5&arch=i386&apropos=0&manpath=OpenBSD+Current).
Also, a nice introductory article can be found
[here](http://www.crypto.com/trustmgt/kn.html).

Although I have developed [pykeynote](https://github.com/argp/pykeynote)
on Linux, and minimally tested it on OpenBSD, it will probably work on all
Unix-like systems that satisfy the following requirements:

* Python version 2.3 or higher. 
* [Pyrex](http://www.cosc.canterbury.ac.nz/greg.ewing/python/Pyrex/)
  version 0.9.4 or higher (optional). 
* The [KeyNote trust management system](http://www1.cs.columbia.edu/~angelos/keynote.html)
  (tested with version 2.3). 
* The [OpenSSL cryptographic toolkit](http://www.openssl.org/)
  (tested with version 0.9.8d).

For the details you can browse the
[repository](https://github.com/argp/pykeynote);
I have included a
[comprehensive testsuite](https://github.com/argp/pykeynote/blob/master/test.py)
and a [sample
application](https://github.com/argp/pykeynote/blob/master/sample_app.py).
