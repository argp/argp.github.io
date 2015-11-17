---
title: Listening to research papers
layout: post
tags:
  - festival
  - mp3
---
A friend recently gave me the nice idea of listening to, instead of reading,
research papers. We both have "to-read" piles that are constantly getting
bigger, even while following the one-paper-per-day rule. Shortly after she
mentioned this to me, I started experimenting with
[Festival](http://www.cstr.ed.ac.uk/projects/festival), the excellent open
source speech synthesis system. I just needed to `emerge festival` on my Gentoo
Linux to get the main engine and `emerge mbrola` to install some extra
natural-sounding voices. I then run
`echo "(set! voice_default 'voice_us1_mbrola)" >> ~/.festivalrc` to change the
default male voice to a female one, and
`echo "Pizza, pizza.  Pizza, pizza." | festival --tts -` as an initial test.
The output was played at double speed. After googling a bit I found the solution
to this problem in the [Festival
FAQ](http://www.cstr.ed.ac.uk/cgi-bin/cstr/lists.cgi?config=festival_faq&#038;entry=arunning_festival/speed.html).

To save the output of Festival to an MP3 file I added the following to my  
`/usr/share/festival/siteinit.scm` file:

{% highlight bash %}
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Required_Rate 11025)
(Parameter.set 'Audio_Required_Format 'riff)
(Parameter.set 'Audio_Command "lame --quiet --preset voice $FILE - >> $HOME/tmp/output.mp3")
{% endhighlight %}

Next, I simply converted some PDF papers into plain text using `pdftotext` and
fed the output to Festival. Although it is true that not all papers can be fully
understood simply by listening to them, this is a way to save significant
amounts of time when it comes to not particularly important papers that nonetheless
have to be read.
