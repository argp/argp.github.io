---
id: 75
title: linksys wrt54gl resurrection
author: argp
layout: post
guid: http://argp.gr/blog/?p=75
permalink: /2008/10/20/linksys-wrt54gl-resurrection/
categories:
  - hacks
tags:
  - hardware
  - linksys
  - openwrt
  - wireless
  - wrt54gl
---
Last week I was experimenting with various changes to [OpenWrt][1] Kamikaze version 7.09 on my [Linksys WRT54GL][2] wireless router. The objective was to modify the Kamikaze firmware for WRT54GL in order to implement a rogue access point for use in various penetration testing contracts. I decided to start the whole endeavor since the [Airsnarf Rogue Squadron][3] firmware only supports the WRT54G model. After a lot of successful firmware flashings during testing, I eventually (and perhaps unavoidably) flashed my router with a corrupted firmware. The result was a dead WRT54GL that was not replying to pings, not even after a hard reset.

To resurrect it I followed [void main&#8217;s WRT54G revival guide][4]. Although the guide was written for the WRT54G model, it is mostly applicable to WRT54GL as well. One of the main differences is that I had to short pins 16 and 17, not 15 and 16 (see the photograph):

<center>
  <a href="http://www.flickr.com/photos/argp/3007982598/"><img src="http://farm4.static.flickr.com/3068/3007982600_a0d5c8a1a1_o.jpg" width="271" height="210" alt="wrt54gl-1-small" /></a>
</center>

A rather important tip is that right after a successful flashing you should always enable the `boot_wait` NVRAM option in order to be able to use the TFTP bootloader. This will save you a lot of time if you are in the edit-compile-upload firmware-debug cycle.

Final note: I was triumphant and there was much rejoicing indeed.

 [1]: http://openwrt.org/
 [2]: http://en.wikipedia.org/wiki/Linksys_WRT54G_series#WRT54GL
 [3]: http://airsnarf.shmoo.com/rogue_squadron/
 [4]: http://voidmain.is-a-geek.net/redhat/wrt54g_revival.html