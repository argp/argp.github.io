---
id: 19
title: irssi last.fm now playing script
author: argp
layout: post
guid: http://argp.gr/blog/?p=19
permalink: /2007/04/28/irssi-lastfm/
categories:
  - code
  - hacks
tags:
  - code
  - irssi
  - last.fm
  - perl
---
I wrote an [irssi][1] script that displays the most recent [last.fm][2] audioscrobbled track. You can find it [here][3]; it is published under a [BSD-style license][4].

The script polls the specified last.fm profile for the most recent audioscrobbled track every `$timeout_seconds` (default is `120`). The track is displayed only in the channels specified in the `@channels` array or, if `@channels` is undefined, in the active window. Be careful if you want to change the value of `$timeout_seconds`; too aggressive polling may get your IP blacklisted.

Put it in `~/.irssi/scripts/lastfm.pl`, load it with `/script load lastfm.pl` and start a new session with `/lastfm start your_lastfm_username`. `/lastfm help` outputs usage details.

Suggestions and bug reports are welcome.

 [1]: http://www.irssi.org/
 [2]: http://www.last.fm/
 [3]: http://ntrg.cs.tcd.ie/~argp/code/attic/lastfm
 [4]: http://www.opensource.org/licenses/bsd-license.php