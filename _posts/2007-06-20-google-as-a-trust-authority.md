---
id: 35
title: 'google as a &#8220;trust authority&#8221;'
author: argp
layout: post
guid: http://argp.gr/blog/?p=35
permalink: /2007/06/20/google-as-a-trust-authority/
aktt_notify_twitter:
  - no
categories:
  - research
  - security
tags:
  - authentication
  - google
  - identification
  - pagerank
  - phishing
  - pki
---
I have recently noticed that I am using Google as a way to avoid phishing websites when I am making online purchases or doing online banking. As an example, to find Bank of Ireland&#8217;s online banking website I avoid to directly type its URL since I can never remember it and a misspelling would most probably lead me to a fake server. Therefore, I simply google the terms &#8220;[365 bank of ireland][1]&#8221; and I am certain that the first result would link to the correct website. Basically, I am using Google as a &#8220;trust authority;&#8221; as an entity that I trust to refer me to the authentic provider I am looking for and not another masquerading as the target provider.

In a traditional PKI setting a Certificate Authority (CA) provides a very similar, in a semantic and not strictly technical sense, service; it gives guarantees to a service consumer that the service provider he is about to disclose sensitive information to is indeed the entity it claims to be. The main difference is that a PKI CA follows a manual way to verify the digital identity of a service provider before it issues an identity certificate (and, [ as I have previously studied][2], they cannot really be trusted on this due to mainly cost reasons). On the other hand, Google relies on an automated way to map keywords to service providers. [PageRank][3] could be modified, or a similar algorithm could be developed, to associate public keys to identities, and rank them in case more than one keys refer to the same identity based on a variety of factors like the time period the key has been associated with the target identity, eigenvector centrality, as well as others.

Actually, [Dimitris Glynos][4] and myself have done some joint research work on the subject and have interesting and encouraging results to share &#8211; not to mention a full Python implementation of our proposed scheme that we plan to release as an open source project running on Linux. But this is the topic of another post.

I am not saying that Google should be trusted with even more power. What I am saying is that the PKI trust model doesn&#8217;t work, particularly as a phishing countermeasure, but also in more general application domains as its limited adoption, among other facts, clearly demonstrates, and that we need to study alternatives.

 [1]: http://www.google.com/search hl=en&#038;lr=&#038;q=365+bank+of+ireland&#038;btnG=Search
 [2]: http://wesii.econinfosec.org/draft.php?paper_id=9
 [3]: http://www.google.com/technology/
 [4]: http://modal-echoes.blogspot.com/