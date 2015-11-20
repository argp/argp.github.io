---
title: Google as a "trust authority"
layout: post
tags:
  - authentication
  - google
  - identification
  - pagerank
  - phishing
  - pki
---
I have recently noticed that I am using Google as a way to avoid phishing 
websites when I am making online purchases or doing online banking. As an 
example, to find Bank of Ireland's online banking website I avoid to 
directly type its URL since I can never remember it and a misspelling would 
most probably lead me to a fake server. Therefore, I simply google the terms 
["365 bank of
ireland"](https://www.google.com/search?num=20&newwindow=1&site=&source=hp&q=365+bank+of+ireland)
and I am certain that the first result would link to the correct website.
Basically, I am using Google as a "trust authority"; as an entity that I
trust to refer me to the authentic provider I am looking for and not another
masquerading as the target provider.

In a traditional PKI setting a Certificate Authority (CA) provides a very 
similar, in a semantic and not strictly technical sense, service; it gives 
guarantees to a service consumer that the service provider he is about to 
disclose sensitive information to, is indeed the entity it claims to be. The 
main difference is that a PKI CA follows a manual way to verify the digital 
identity of a service provider before it issues an identity certificate (and,
[as I have previously
studied](http://citeseerx.ist.psu.edu/viewdoc/download?rep=rep1&type=pdf&doi=10.1.1.215.1496),
they cannot really be trusted on this due to mainly cost reasons). On the
other hand, Google relies on an automated way to map keywords to service
providers. [PageRank](https://en.wikipedia.org/wiki/PageRank) could be modified,
or a similar algorithm could be developed, to associate public keys to identities, 
and rank them in case more than one keys refer to the same identity based on a 
variety of factors like the time period the key has been associated with the 
target identity, eigenvector centrality, as well as others.

Actually, Dimitris Glynos and myself have done some joint research work on 
the subject and have interesting and encouraging results to share - not to
mention a full Python implementation of our proposed scheme that we plan to 
release as an open source project running on Linux. But this is the topic of 
another post.

I am not saying that Google should be trusted with even more power. What I am 
saying is that the PKI trust model doesn't work, particularly as a phishing
countermeasure, but also in more general application domains as its limited
adoption, among other facts, clearly demonstrates, and that we need to 
study alternatives.
