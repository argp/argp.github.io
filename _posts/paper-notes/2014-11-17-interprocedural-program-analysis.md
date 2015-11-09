---
id: 4656
title: Interprocedural program analysis
author: argp
layout: post
guid: http://sysc.tl/?p=4656
permalink: /2014/11/17/interprocedural-program-analysis/
categories:
  - paper notes
tags:
  - interprocedural
  - program analysis
---
I have been reading/thinking about interprocedural (binary mostly) program analysis lately. There are two ways to do it: a) function summaries produced in advance; b) inlining function bodies and (try to) do whole-program analysis. The problem with a) is (possible) reduced accuracy, and with b) scalability.

Have I missed something? Any pointers to relevant work?

Program analysis Jedi <a href="https://twitter.com/jvanegue" target="_blank">@jvanegue</a> suggested <a href="http://research.microsoft.com/en-us/projects/slam/" target="_blank">SLAM</a> and <a href="http://asa.iti.kit.edu/daikon.pdf" target="_blank">Daikon</a>.

Relevant Twitter link: <a href="https://twitter.com/_argp/statuses/514491405142863872" target="_blank">https://twitter.com/_argp/statuses/514491405142863872</a>