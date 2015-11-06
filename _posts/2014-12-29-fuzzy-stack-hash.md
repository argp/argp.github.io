---
title: Fuzzy stack hash
layout: post
tags:
  - paper notes
  - crash analysis
  - fuzzing
  - triage
---
If you have done any large scale fuzzing then you have faced the problem of duplicate bugs. These take time to be manually recognized and marked as duplicates.

I have been discussing this recently with fellow CENSUS researcher <a href="https://twitter.com/anestisb" target="_blank">@anestisb</a> (be sure to check out and vote for <a href="https://www.syscan.org/index.php/sg/cfp/vote/" target="_blank">his SyScan 2015 submission</a> on fuzzing and the internals of the new Android L runtime). 

We have reached the conclusion that the &#8220;fuzzy stack hash&#8221; provides an easily configurable trade-off to automatically identify semantically duplicate bugs. You can find its full description in the otherwise also very interesting paper <a href="http://cpl0.net/~argp/papers/50a11f65857c12c76995f843dbfe6dda.pdf" target="_blank">&#8220;Dynamic test generation to find integer bugs in x86 binary linux programs&#8221;</a>, section 6.1, page 9. 

The information used in the calculation of the fuzzy stack hash are a) the name of the function in which the crash occurred (or its address if no debug symbols are available), b) the source code line number if available (excluding the last digit to allow for changes in the code), and c) the name of the object file for each frame in the call stack. The hash is calculated over all these for N functions on the top of the call stack at the crash. N determines the &#8220;fuzzy-ness&#8221; of the hash and provides us with a configurable trade-off. A small N leads to labelling as duplicates different bugs that cause a crash at the same location; a large value for N leads to the fuzzy stack hash being essentially a normal backtrace leading to duplicate bugs being labelled as unique.
