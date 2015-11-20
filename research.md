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
Miami, USA, April 2015. [[slides]](https://speakerdeck.com/argp/orlyeh-the-shadow-over-firefox)
[[code]](https://github.com/CENSUS/shadow)
* [SummerCon](http://web.archive.org/web/20150919005103/http://www.summercon.org/presentations.html#firefox),
New York, USA, July 2015.

### Project Heapbleed

> Heap related bugs (such as buffer overflows, use-after-frees, dangling/stale
> pointers, double frees) leading to corruptions of virtual memory and vulnerable
> conditions, constitute the most common type of memory corruption bugs. The
> exploitation of heap vulnerabilities is a process that requires a lot of time and
> effort. It requires meticulous understanding of the underlying heap allocator; its
> data structures (metadata) and its allocation/deallocation algorithms. It requires
> understanding of how the target application uses the API provided by the heap
> allocator to manage dynamic memory and the allocation patterns that emerge due
> to this use. It also requires understanding of the application-specific data and
> how/where these are placed on the heap. Finally, it requires studying of the way
> the user can influence the application and use its provided functionality to
> control its heap as reliably as possible with the goal to create conditions aiding
> exploitation. All these must be viewed in the context of complicated bugs, since
> low-hanging fruits are scarce, and the vendors' adoption of increasingly
> sophisticated exploitation mitigation technologies. We argue that although the
> details between the different heap allocators, target applications and bugs at hand
> obviously vary, the heap exploitation methodologies that have been formed by
> practical experience can be abstracted to reusable primitives that can be applied
> to new targets. Project Heapbleed is our attempt to define, clearly articulate,
> categorize and where applicable implement these primitives, aiming to provide a
> practical reusable heap exploitation toolset.

* [ZeroNights](http://2014.zeronights.org/conference/agenda.html#patroklos),
Moscow, Russia, November 2014. [[slides]](https://speakerdeck.com/argp/project-heapbleed)
[[video]](https://www.youtube.com/watch?v=IAFqhzNgJgI)
* [BalCCon](https://2k14.balccon.org/index.php?title=Project_Heapbleed), Novi Sad,
Serbia, September 2014. [[video]](https://www.youtube.com/watch?v=-smvfojecvs)

### Firefox Exploitation

> The Mozilla Firefox web browser has a new memory allocator named 'jemalloc'
> enabled by default on all supported platforms (Windows, OS X, Linux, Android
> and Firefox OS). Therefore, the traditional platform-specific heap exploitation
> techniques (like unlinkink and frontlinking) are no longer applicable
> when attacking new Firefox heap corruption vulnerabilities. In this talk
> we will develop novel exploitation approaches and primitives that can be
> used to attack Mozilla Firefox via its new heap manager. We will build on
> our previously published work on this area and include practical hands-on
> demonstrations of researching Firefox vulnerabilities and developing
> exploits for them. Moreover, we will release an updated and enhanced version
> of our jemalloc debugging utility ('unmask_jemalloc').

* [AthCon](http://cc.thinkst.com/conference/view/656/), Athens, Greece, June 2013.
[[slides]](https://speakerdeck.com/argp/firefox-exploitation)
[[code]](https://github.com/argp/unmask_jemalloc)

### Exploiting the jemalloc Memory Allocator: Owning Firefox's Heap
#### with Chariton Karamitas

> jemalloc is a userland memory allocator that is being increasingly adopted
> by software projects as a high performance heap manager. It is used in
> Mozilla Firefox for the Windows, Mac OS X and Linux platforms, and as the
> default system allocator on the FreeBSD and NetBSD operating systems.
> Facebook also uses jemalloc in various components to handle the load of its
> web services. However, despite such widespread use, there is no work on the
> exploitation of jemalloc.
>
> Our research addresses this. We will begin by examining the architecture of
> the jemalloc heap manager and its internal concepts, while focusing on
> identifying possible attack vectors. jemalloc does not utilize concepts such
> as unlinking or frontlinking that have been used extensively in the past
> to undermine the security of other allocators. Therefore, we will develop
> novel exploitation approaches and primitives that can be used to attack
> jemalloc heap corruption vulnerabilities. As a case study, we will investigate
> Mozilla Firefox and demonstrate the impact of our developed exploitation
> primitives on the browser's heap. In order to aid the researchers willing to
> continue our work, we will also release our jemalloc debugging tool belt.

* [Black Hat USA](https://www.blackhat.com/html/bh-us-12/bh-us-12-briefings.html#Argyroudis),
Las Vegas, USA, July 2012.
[[slides]](https://speakerdeck.com/argp/exploiting-the-jemalloc-memory-allocator-owning-firefoxs-heap)
[[code]](https://github.com/argp/unmask_jemalloc)
