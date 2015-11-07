---
id: 274
title: 'Let&#8217;s make email more secure, a simple suggestion'
author: argp
layout: post
guid: http://argp.gr/blog/?p=274
permalink: /2004/09/02/secure-email-suggestion/
aktt_notify_twitter:
  - no
categories:
  - research
  - security
tags:
  - authentication
  - email
  - research
  - security
  - smtp over tls
---
No, this post will not discuss possible solutions to the problem of spam. If you are interested in such proposals be sure to check out [LOAF][1], an elegant system based on social networking ideas.

My suggestion concerns something far more simple. Message delivery. Think what happens when you send an email. Your email client delivers the outgoing message to the email server of your local domain (like your ISP&#8217;s or university&#8217;s email server). This email server then contacts the email server of the recipient&#8217;s domain and forwards the message there. When the recipient checks for new messages using her email client she retrieves your email. Actually this is the best case scenario. There may be more domain email servers in between. My suggestion is simply to change the behavior of email clients in order to deliver messages directly to the email server of the recipient, avoiding the initial unnecessary step of temporarily storing messages on the sender&#8217;s domain email server.

Now, let&#8217;s take this a step further. DSL and cable connections are quickly becoming pervasive. Most Internet users are now having constant connections. This allows the operation of email servers on the users&#8217; computers, enabling the delivery of email messages directly from the sender to the recipient. Of course, in order to be sure that no messages are lost the ISP of the user can provide a secondary email server to store incoming messages in the case the user has turned off his computer.

Since we came this far, why not go all the way? The main problem of [SMTP over TLS][2] is that it does not offer end-to-end security, since the establishment of a TLS session between two email servers does not mean that the entire SMTP chain from the sender to the recipient has been secured. However, if we implement my suggestion from the previous paragraph we have just solved this problem.

I am aware that all these cannot and will not happen overnight. However, I think that my first suggestion regarding the delivery of email messages from the client utility of the sender to the email server of the recipient&#8217;s domain is a realistic one that can easily be implemented. And this small first step will bring us closer to what we all want, end-to-end secure email.

 [1]: http://loaf.cantbedone.org/
 [2]: http://www.ietf.org/rfc/rfc2487.txt