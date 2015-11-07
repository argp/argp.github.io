---
id: 284
title: Datagram TLS and the Authorization eXchange Protocol (AXP)
author: argp
layout: post
guid: http://argp.gr/blog/?p=284
permalink: /2005/08/30/datagram-tls-axp/
aktt_notify_twitter:
  - no
categories:
  - research
  - security
tags:
  - authorization
  - axp
  - cryptography
  - dtls
  - æther
---
The [OpenSSL repository][1] now includes [Datagram TLS (DTLS)][2] support. More than a year ago I designed and implemented a security protocol for the NTRG ad hoc networking stack that uses UDP at the transport layer, the [Authorization eXchange Protocol (AXP)][3]. The main goal of AXP is to provide a modular and extensible solution to the problem of exchanging authorization credentials. If I had DTLS back then it would have made my life so much easier. I would have simply focused on the problem that I was interested in, flexibility in transmitting and receiving service access requests and replies along with the credentials that are required to support them, instead of spending huge amounts of time designing and coding an SSL/TLS alternative for datagram transport protocols.

 [1]: http://dev.openssl.org/source/repos.html
 [2]: http://crypto.stanford.edu/~nagendra/papers/dtls.pdf
 [3]: http://doi.ieeecomputersociety.org/10.1109/ISCC.2005.146