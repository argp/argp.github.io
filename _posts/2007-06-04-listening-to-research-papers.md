---
id: 30
title: listening to research papers
author: argp
layout: post
guid: http://argp.gr/blog/?p=30
permalink: /2007/06/04/listening-to-research-papers/
categories:
  - research
tags:
  - festival
  - mp3
---
A friend recently gave me the nice idea of listening to, instead of reading, research papers. We both have &#8220;to-read&#8221; piles that are constantly getting bigger, even while following the one-paper-per-day rule. Shortly after she mentioned this to me, I started experimenting with [Festival][1], the excellent open source speech synthesis system. I just needed to `emerge festival` on my Gentoo Linux to get the main engine and `emerge mbrola` to install some extra natural-sounding voices. I then run `echo "(set! voice_default 'voice_us1_mbrola)" >> ~/.festivalrc` to change the default male voice to a female one, and `echo "Pizza, pizza.  Pizza, pizza." | festival --tts -` as an initial test. The output was played at double speed. After googling a bit I found the solution to this problem in the [Festival FAQ][2].

To save the output of Festival to an MP3 file I added the following to my  
`/usr/share/festival/siteinit.scm` file:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">&#40;</span>Parameter.set <span style="color: #ff0000;">'Audio_Method '</span>Audio_Command<span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#40;</span>Parameter.set <span style="color: #ff0000;">'Audio_Required_Rate 11025)
(Parameter.set '</span>Audio_Required_Format <span style="color: #ff0000;">'riff)
(Parameter.set '</span>Audio_Command <span style="color: #ff0000;">"lame --quiet --preset voice <span style="color: #007800;">$FILE</span> - &gt;&gt; <span style="color: #007800;">$HOME</span>/tmp/output.mp3"</span><span style="color: #7a0874; font-weight: bold;">&#41;</span></pre>
      </td>
    </tr>
  </table>
</div>

Next, I simply converted some PDF papers into plain text using `pdftotext` and fed the output to Festival. Although it is true that not all papers can be fully understood simply by listening to them, this is a way to save significant amounts of time when it comes to not particularly important papers that nonetheless have to be read.

 [1]: http://www.cstr.ed.ac.uk/projects/festival
 [2]: http://www.cstr.ed.ac.uk/cgi-bin/cstr/lists.cgi?config=festival_faq&#038;entry=arunning_festival/speed.html