---
layout: page
title: research
---

*Note: Incomplete; more will be added later.*

### Vs com.apple.security.sandbox

> The iOS sandbox kernel extension implements one of the fundamental security
> technologies deployed on Apple's devices (iPhones, iPads, etc.) for limiting
> local privilege escalation and post-exploitation. The sandbox utilizes
> Apple-specified policies to restrict what operations both system-provided
> services and user-installed applications can perform. The sandbox kernel
> extension is closed-source both on iOS and macOS; furthermore the iOS sandbox
> policies are not available in plain text, but compiled and packed in the binary
> of the extension itself. In this talk I will initially present how the iOS
> sandbox kernel extension specifies and enforces policies, along with
> implementation details that will be useful for the next step. I will then
> explain in detail the process of reverse engineering the extension in order to
> unpack and decompile all the sandbox policies embedded in it. All the presented
> details apply to and have been tested on the latest iOS version (12.1.3 beta 2
> at the time of this writing).

* [CanSecWest](https://cansecwest.com/post/2019-02-07-20:00:00_2019_Speakers),
Vancouver, Canada, March 2019. [[slides]](https://speakerdeck.com/argp/vs-com-dot-apple-dot-security-dot-sandbox)
* [0x41con](https://0x41con.eu/), Amsterdam, the Netherlands, May 2019.

### iOS Kernel Exploitation Archaeology

> The evasi0n7 jailbreak was released by the evad3rs on 22nd December 2013
> targeting devices running iOS 7.0 to 7.1b3. This talk documents the
> reverse engineering process of evasi0n7's main kernel exploit, which was
> performed in order to not only understand the underlying vulnerability, but
> more importantly to document the exploitation techniques the evad3rs have
> utilized. The talk will initially focus on the kernel debugging setup (a
> very important but often ignored step in device/embedded exploitation
> talks), the encountered problems and how they were overcome. I will then
> explain the underlying vulnerability, and the reverse engineering of the
> implemented exploitation techniques. Finally, I will present a detailed
> step-by-step re-implementation of the kernel exploit.

* [34th Chaos Communication Congress
(34C3)](https://events.ccc.de/congress/2017/Fahrplan/events/8720.html),
Leipzig, Germany, December 2017. [[slides]](https://speakerdeck.com/argp/ios-kernel-exploitation-archaeology)
[[video]](https://media.ccc.de/v/34c3-8720-ios_kernel_exploitation_archaeology)
* [WarCon](http://warcon.pl/2017/), Warsaw, Poland, June 2017.

### The Shadow over Android: Heap Exploitation Assistance <br/> &nbsp;&nbsp;&nbsp;&nbsp;for Android's libc Allocator
&mdash; with Vasilis Tsaousoglou

> The jemalloc allocator has been adopted as the default libc malloc(3)
> implementation on Android since version 5.0, and is being used up to the
> latest one (7.0 - Nougat). We have previously analyzed in depth memory
> corruption attacks against jemalloc as a standalone allocator and in the
> context of the Firefox browser. In this talk we will focus on presenting
> attacks against jemalloc as the main userland allocator of Android devices
> (smartphones and tablets). We have extended our jemalloc heap exploration
> and exploitation tool called 'shadow' to support Android (both ARM32 and
> ARM64), and we will be demonstrating its use on understanding the impact of
> heap corruption vulnerabilities and developing exploits for them. The new
> version of shadow (supporting Android ARM32/ARM64 and Firefox x86/x86-64)
> will be released as open source software along with the talk.

* [INFILTRATE Security Conference](http://www.infiltratecon.org/archives/), Miami, USA,
April 2017. [[slides]](https://speakerdeck.com/argp/the-shadow-over-android)
[[code]](https://github.com/CENSUS/shadow)

### Keynote: Reflections on vulnerability research; <br/> &nbsp;&nbsp;&nbsp;&nbsp;is the only winning move not to play?

* [Hackers to Hackers Conference (H2HC)](https://www.h2hc.com.br/h2hc/en/eventos),
Sao Paulo, Brazil, October 2016.

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

* [Phrack](http://www.phrack.org/), [OR'LYEH? The Shadow over
Firefox](http://www.phrack.org/issues/69/14.html#article), Volume 0x0f, Issue 0x45.
* [INFILTRATE Security Conference](http://www.infiltratecon.org/archives/), Miami, USA,
April 2015. [[slides]](https://speakerdeck.com/argp/orlyeh-the-shadow-over-firefox)
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

### Exploiting the jemalloc Memory Allocator: Owning Firefox's Heap
&mdash; with Chariton Karamitas

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

* [Phrack](http://www.phrack.org/), [Pseudomonarchia
jemallocum](http://www.phrack.org/issues/68/10.html#article), Volume 0x0e, Issue 0x44.
* [Phrack](http://www.phrack.org/), [The Art of Exploitation: Exploiting
VLC](http://www.phrack.org/issues/68/13.html#article), Volume 0x0e, Issue 0x44.
* [Black Hat USA](https://www.blackhat.com/html/bh-us-12/bh-us-12-briefings.html#Argyroudis),
Las Vegas, USA, July 2012.
[[slides]](https://speakerdeck.com/argp/exploiting-the-jemalloc-memory-allocator-owning-firefoxs-heap)
[[code]](https://github.com/argp/unmask_jemalloc)
* [AthCon](http://cc.thinkst.com/conference/view/656/), Athens, Greece, June 2013.
[[slides]](https://speakerdeck.com/argp/firefox-exploitation)

### Heap Exploitation Abstraction by Example
&mdash; with Chariton Karamitas

> In the first part of the talk we focused on presenting examples of exploiting heap
> managers. Specifically, we talked about attacking the FreeBSD kernel allocator
> (UMA), the Linux kernel allocator (SLUB), and the jemalloc userland allocator. In
> the second part, we identified the common elements of these three allocators and
> categorized them into the following:
>
> * End-user allocations
> * Allocation containers
> * Container groupings
> * Execution-specific (thread, CPU core) metadata
>
> We then proceeded to make an argument that the value of abstracting heap
> exploitation is in having a library of attack techniques, or primitives, that
> can be reused on other allocators. We took the concept of weird machines, as
> defined by Sergey Bratus and Halvar Flak, and applied it to heap managers.
> We consider an allocator to be a deterministic automaton; metadata
> corruption attacks can then be viewed as corruptions of the automaton's
> transition function. Application-specific attacks, like adjacent memory region
> corruptions, can be viewed as manipulations of the automaton's determinacy.

* [OWASP AppSec Research](http://2012.appsec.eu/schedule/index.html), Athens,
Greece, July 2012. [[slides]](https://speakerdeck.com/argp/heap-exploitation-abstraction-by-example)
* [FOSSCOMM](http://census-labs.com/news/2011/05/17/fosscomm-2011/),
Patras, Greece, May 2011. [[slides]](https://speakerdeck.com/argp/patras-heap-massacre)

### Protecting the Core: Kernel Exploitation Mitigations
&mdash; with Dimitrios Glynos

> The exploitation of operating system kernel vulnerabilities has received a
> great deal of attention lately. In userland most generic exploitation
> approaches have been defeated by countermeasure technologies. Contrary to
> userland protections, exploitation mitigation mechanisms for kernel memory
> corruptions have not been widely adopted. Recently this has started to
> change. Most operating system kernels have started to include
> countermeasures against NULL page mappings, stack and heap corruptions, as
> well as for other vulnerability classes. At the same time, researchers
> have concentrated on developing ways to bypass certain kernel protections
> on various operating systems. This presentation will describe in detail
> the state-of-the-art in kernel exploitation mitigations adopted (or not)
> by various operating systems (Windows, Linux, Mac OS X, FreeBSD) and
> mobile platforms (iOS, Android). Moreover, it will also provide
> approaches, notes, hints and references to existing work for bypassing
> some of these kernel protections.

* [Black Hat
Europe](https://www.blackhat.com/html/bh-eu-11/bh-eu-11-briefings.html#Argyroudis),
Barcelona, Spain, March 2011.
[[slides]](https://speakerdeck.com/argp/protecting-the-core-kernel-exploitation-mitigations)

### Binding the Daemon: FreeBSD Kernel Stack and Heap Exploitation

> FreeBSD is widely accepted as one of the most reliable and performance-driven
> operating systems currently available in both the open source and proprietary
> worlds. While the exploitation of kernel vulnerabilities has been researched
> in the context of the Windows and Linux operating systems, FreeBSD, and BSD
> systems in general, have not received the same attention. This presentation
> will initially examine the exploitation of kernel stack overflow vulnerabilities
> on FreeBSD. The development process of a privilege escalation kernel stack
> smashing exploit will be documented for vulnerability CVE-2008-3531. The second
> part of the presentation will present a detailed security analysis of the
> Universal Memory Allocator (UMA), the FreeBSD kernel's memory allocator.
> We will examine how UMA overflows can lead to arbitrary code execution in
> the context of the latest stable FreeBSD kernel (8.0-RELEASE), and we will
> develop an exploitation methodology for privilege escalation and kernel
> continuation.

* [Phrack](http://www.phrack.org/), [Exploiting UMA, FreeBSD's kernel memory
allocator](http://www.phrack.org/issues/66/8.html#article), Volume 0x0d, Issue 0x42.
* [Black Hat
Europe](https://www.blackhat.com/html/bh-eu-10/bh-eu-10-briefings.html#Argyroudis),
Barcelona, Spain, April 2010.
[[slides]](https://speakerdeck.com/argp/binding-the-daemon-freebsd-kernel-stack-and-heap-exploitation)
[[paper]](/public/binding-the-daemon-wp.pdf)
[[code]](https://github.com/argp/binding-the-daemon)
* [PH-Neutral](http://ph-neutral.darklab.org/previous/0x7db/talks.html),
Berlin, Germany, May 2011. [[slides]](https://speakerdeck.com/argp/freebsd-kernel-massacre)
* [University of Piraeus](http://rainbow.cs.unipi.gr/projects/oss/wiki/EventSixteen), Athens,
Greece, May 2008. [[slides
(in greek)]](https://speakerdeck.com/argp/tekhnikes-ekmetalleuses-trototeton-asphaleias-purena)

-------

*For my older academic publications see [my Google Scholar
page](https://scholar.google.com/citations?user=6IUnc4EAAAAJ).*
