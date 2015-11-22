---
title: Linksys WRT54GL resurrection
layout: post
tags:
  - hardware
  - linksys
  - openwrt
  - wireless
  - wrt54gl
---
Last week I was experimenting with various changes to
[OpenWrt](//openwrt.org/) Kamikaze version 7.09 on my
[Linksys WRT54GL](http://en.wikipedia.org/wiki/Linksys_WRT54G_series#WRT54GL)
wireless router. The objective was to modify the Kamikaze firmware for WRT54GL
in order to implement a rogue access point for use in various penetration
testing contracts. I decided to start the whole endeavor since the
[Airsnarf Rogue Squadron](http://airsnarf.shmoo.com/rogue_squadron/)
firmware only supports the WRT54G model. After a lot of successful firmware
flashings during testing, I eventually (and perhaps unavoidably) flashed my
router with a corrupted firmware. The result was a dead WRT54GL that was not
replying to pings, not even after a hard reset.

To resurrect it I followed [void main's WRT54G revival
guide](http://voidmain.is-a-geek.net/redhat/wrt54g_revival.html). Although the
guide was written for the WRT54G model, it is mostly applicable to WRT54GL as
well. One of the main differences is that I had to short pins 16 and 17, not
15 and 16 (see the photograph):

<p align="center">
<img src="http://farm4.static.flickr.com/3068/3007982600_a0d5c8a1a1_o.jpg"/>
</p>

A rather important tip is that right after a successful flashing you should 
always enable the `boot_wait` NVRAM option in order to be able to use the TFTP 
bootloader. This will save you a lot of time if you are in the 
"edit-compile-upload firmware-debug" loop.
