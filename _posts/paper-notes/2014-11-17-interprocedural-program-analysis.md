---
layout: post
title: "Paper notes: Interprocedural program analysis"
tags:
  - paper notes
  - interprocedural
  - program analysis
---
I have been reading/thinking about interprocedural (binary mostly) program
analysis lately. There are two ways to do it: a) function summaries produced
in advance; b) inlining function bodies and (try to) do whole-program analysis.
The problem with a) is (possible) reduced accuracy, and with b) scalability.

Have I missed something? Any pointers to relevant work?

Program analysis Jedi <a href="https://twitter.com/jvanegue">@jvanegue</a>
suggested <a href="http://research.microsoft.com/en-us/projects/slam/">SLAM</a>
and <a href="http://asa.iti.kit.edu/daikon.pdf">Daikon</a>.

Relevant Twitter link:
<a href="https://twitter.com/_argp/statuses/514491405142863872">https://twitter.com/_argp/statuses/514491405142863872</a>
