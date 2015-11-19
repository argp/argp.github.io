---
layout: page
title: research
---

*Note: Incomplete; more will be added later.*

### OR’LYEH? The Shadow over Firefox

> The Mozilla Firefox browser has a new garbage collection (GC) implementation
> for its JavaScript engine (SpiderMonkey) since version 32. This new GC algorithm
> has introduced significant changes to the way that Firefox's heap is organized.
> The GC heap is now divided into two layers; a first layer for short-lived
> objects, called the 'nursery', and a second layer for objects that survived
> a GC pass in the nursery, called the 'tenured' heap. Apart from these two, the
> latest version of Firefox continues to use jemalloc (on all its supported platforms)
> for SpiderMonkey metadata and GC heap objects that fit certain criteria. These
> changes directly affect the way that the browser's heap can be manipulated towards
> states that aid in the exploitation of heap vulnerabilities.
>
> In this talk we will expand upon previous work we have published on jemalloc heap
> exploitation approaches and primitives for Firefox, taking into account its new
> GC heap implementation. The presentation will demonstrate a major upgrade of our
> 'unmask_jemalloc' Firefox heap exploration utility with new features, and support
> for Windows (and the WinDbg debugger). The new version of unmask_jemalloc, named
> 'shadow', will of course be released as open source along with the talk.

* [INFILTRATE Security
Conference](http://web.archive.org/web/20150315014310/http://www.infiltratecon.com/speakers.html#firefox),
Miami Beach, USA, April 2015. [[slides](https://speakerdeck.com/argp/orlyeh-the-shadow-over-firefox)]
* [SummerCon 2015](http://web.archive.org/web/20150919005103/http://www.summercon.org/presentations.html#firefox),
New York, USA, July 2015.
