---
title: irssi last.fm now playing script
layout: post
tags:
  - code
  - irssi
  - last.fm
  - perl
---
I wrote an [irssi](http://www.irssi.org/) script that displays the most
recent [last.fm](http://www.last.fm/) audioscrobbled track. You can find
it [here](https://github.com/argp/lastfm-irssi); it is published under a
[BSD-style license](http://www.opensource.org/licenses/bsd-license.php).

The script polls the specified last.fm profile for the most recent
audioscrobbled track every `$timeout_seconds` (default is `120`). The
track is displayed only in the channels specified in the `@channels`
array or, if `@channels` is undefined, in the active window. Be careful
if you want to change the value of `$timeout_seconds`; too aggressive
polling may get your IP blacklisted.

Put it in `~/.irssi/scripts/lastfm.pl`, load it with `/script load lastfm.pl`
and start a new session with `/lastfm start your_lastfm_username`.
`/lastfm help` outputs usage details.

Suggestions and bug reports are welcome.
