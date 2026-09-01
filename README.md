# Awesome eBPF with stars

> A curated list of awesome projects related to eBPF.

BPF, as in *Berkeley Packet Filter*, is an in-kernel virtual machine running programs passed from user space. Initially implemented on BSD, then Linux, the (now legacy) "classic BPF" or cBPF machine would be used with tools like tcpdump for filtering packets in the kernel to avoid useless copies to user space. The BPF infrastructure in Linux was completely reworked and gave life to eBPF, which gained new features (safety and termination checks, JIT-compiling for programs, persistent maps, a standard library, hardware offload support, etc.) and is now used for many tasks. Processing packets at a very low level (XDP), tracing and monitoring events on the system, or enforcing access control over cgroups are but a few examples to which eBPF brings performance, programmability and flexibility.

[Cilium](https://cilium.io) has a great website about eBPF called [ebpf.io](https://ebpf.io/). It serves a similar purpose to this list, with [an introduction to eBPF](https://ebpf.io/what-is-ebpf) and links to [related projects](https://ebpf.io/projects).

> Note: eBPF is an exciting piece of technology, and its ecosystem is constantly evolving. We'd love help from *you* to keep this awesome list up to date, and improve its signal-to-noise ratio in anyway we can. Please feel free to leave [any feedback](https://github.com/qmonnet/awesome-ebpf/issues) ⭐ 5,153 | 🐛 13 | 📅 2026-08-12.

## Contents

* [Reference Documentation](#reference-documentation)
* [Articles and Presentations](#articles-and-presentations)
* [Tutorials](#tutorials)
* [Examples](#examples)
* [eBPF Workflow: Tools and Utilities](#ebpf-workflow-tools-and-utilities)
* [Projects Related to eBPF](#projects-related-to-ebpf)
* [eBPF in Security](#ebpf-in-security)
* [The Code](#the-code)
* [Development and Community](#development-and-community)
* [Other Lists of Resources on eBPF](#other-lists-of-resources-on-ebpf)
* [Acknowledgement](#acknowledgement)

## Reference Documentation

### eBPF Essentials

* [ebpf.io](https://ebpf.io/) - A gateway to discover all the basics of eBPF, including a listing of the main related projects and of community resources.
* [Cilium's BPF and XDP Reference Guide](http://docs.cilium.io/en/latest/bpf/) - In-depth documentation about most features and aspects of eBPF.
* [docs.ebpf.io](https://docs.ebpf.io/) - Providing technical documentation for eBPF.

### Kernel Documentation

* [BPF Documentation](https://www.kernel.org/doc/html/latest/bpf/index.html) - Index for BPF-related documentation coming with the Linux kernel.
* [linux/Documentation/networking/filter.rst](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/networking/filter.rst) - eBPF specification (somewhat outdated; information should still be valid, but not exhaustive).
* [BPF Design Q\&A](https://www.kernel.org/doc/html/latest/bpf/bpf_design_QA.html) - Frequently Asked Questions on the decisions behind the BPF infrastructure.
* [HOWTO interact with BPF subsystem](https://www.kernel.org/doc/html/latest/bpf/bpf_devel_QA.html) - Frequently Asked Questions about contributing to eBPF development.

### Manual Pages

* [`bpf(2)`](http://man7.org/linux/man-pages/man2/bpf.2.html) - Manual page about the `bpf()` system call, used to manage BPF programs and maps from userspace.
* [`tc-bpf(8)`](http://man7.org/linux/man-pages/man8/tc-bpf.8.html) - Manual page about using BPF with tc, including example commands and samples of code.
* [`bpf-helpers(7)` man page](http://man7.org/linux/man-pages/man7/bpf-helpers.7.html) - Description of the in-kernel helper functions forming the BPF standard library.

### Other

* [RFC 9669 BPF Instruction Set Architecture](https://www.rfc-editor.org/rfc/rfc9669.html) - IETF specification for eBPF

* [Jesper Dangaard Brouer's documentation](https://prototype-kernel.readthedocs.io/en/latest/bpf/index.html) - Work in progress, contributions welcome.

* Emails from David Miller to the [xdp-newbies](http://vger.kernel.org/vger-lists.html#xdp-newbies) mailing list:

  * [bpf.h and you...](https://www.spinics.net/lists/xdp-newbies/msg00179.html)
  * [Contextually speaking...](https://www.spinics.net/lists/xdp-newbies/msg00181.html)
  * [BPF Verifier Overview](https://www.spinics.net/lists/xdp-newbies/msg00185.html)

* [List of BPF features per kernel version](https://github.com/iovisor/bcc/blob/master/docs/kernel-versions.md) ⭐ 22,650 | 🐛 1,073 | 🌐 C | 📅 2026-08-27

* [A List of Research Papers](https://pchaigno.github.io/bpf/2025/01/07/research-papers-bpf.html)

## Articles and Presentations

### Generic eBPF Presentations and Articles

If you are new to eBPF, you may want to try the links described as "introductions" in this section.

* [A BPF reference guide](https://github.com/iovisor/bcc/blob/master/docs/reference_guide.md) ⭐ 22,650 | 🐛 1,073 | 🌐 C | 📅 2026-08-27 - About BPF C and bcc Python helpers, from bcc repository.

* [Beginner's guide to eBPF](https://github.com/lizrice/ebpf-beginners) ⭐ 1,730 | 🐛 3 | 🌐 Python | 📅 2023-05-08 - A set of live-coding talks and the accompanying code examples, introducing eBPF programming using a variety of libraries and program types.

* [A brief introduction to XDP and eBPF](https://blogs.igalia.com/dpino/2019/01/07/introduction-to-xdp-and-ebpf/) - An accessible introduction providing context, history, and details about the functioning of eBPF.

* An eBPF Overview - Blog series by Adrian Ratiu, covering many aspects of the eBPF infrastructure:

  * [Part 1: Introduction](https://www.collabora.com/news-and-blog/blog/2019/04/05/an-ebpf-overview-part-1-introduction/)
  * [Part 2: Machine & Bytecode](https://www.collabora.com/news-and-blog/blog/2019/04/15/an-ebpf-overview-part-2-machine-and-bytecode/)

* [Ferris Ellis's blog posts about eBPF](https://ferrisellis.com/tags/ebpf/) - They have a few posts about eBPF:
  * [Part 1: Past, Present, and Future](https://ferrisellis.com/content/ebpf_past_present_future/)
  * [Part 2: Syscall and Map Types](https://ferrisellis.com/content/ebpf_syscall_and_maps/)

* [The BSD Packet Filter](https://speakerdeck.com/tuxology/the-bsd-packet-filter) - An introduction mostly covering the tracing aspects.

* [BPF: tracing and more](https://www.slideshare.net/slideshow/bpf-tracing-and-more/71128334) - An introduction mostly covering the tracing aspects.

* [Linux BPF Superpowers](https://www.slideshare.net/slideshow/linux-bpf-superpowers/58986111) - An introduction mostly covering the tracing aspects, first part with flame graphs.

* [IO Visor](https://www.socallinuxexpo.org/sites/default/files/presentations/Room%20211%20-%20IOVisor%20-%20SCaLE%2014x.pdf) - Also introduces [IO Visor project](https://www.iovisor.org/).

* [BPF -- in-kernel virtual machine](http://vger.kernel.org/netconf2015Starovoitov-bpf_collabsummit_2015feb20.pdf) - Presentation by the author of eBPF.

* [Extending extended BPF](https://lwn.net/Articles/603983/) - A blog post from 2014 on the development of BPF and demonstrating what can be done with it, using an example of stateful socket filtering by attaching an eBPF program to a socket.

* Greg Marsden made some documentation about eBPF:
  * [A Tour of Program Types](https://blogs.oracle.com/linux/post/bpf-a-tour-of-program-types) - A description of all existing hooks for BPF program types, and of their interest.
  * [BPF helper functions](https://blogs.oracle.com/linux/post/bpf-in-depth-bpf-helper-functions) - A review of the kernel functions that can be called from within eBPF programs.
  * [Communicating with Userspace](https://blogs.oracle.com/linux/post/bpf-in-depth-communicating-with-userspace) - How BPF communicates with userspace - BPF maps, perf events, bpf\_trace\_printk.
  * [Building BPF Programs](https://blogs.oracle.com/linux/post/bpf-in-depth-building-bpf-programs) - Setting up your environment to build BPF programs.
  * [The BPF Bytecode and the BPF Verifier](https://blogs.oracle.com/linux/post/bpf-in-depth-the-bpf-bytecode-and-the-bpf-verifier) - How does BPF ensure that programs are safe?
  * [Using BPF to do Packet Transformation](https://blogs.oracle.com/linux/post/bpf-using-bpf-to-do-packet-transformation) - One eBPF usage about packet transformation.

* [Linux Kernel Observability through eBPF](https://sematext.com/blog/linux-kernel-observability-ebpf/) - A blog post covering the basics of eBPF as well as code samples in Go on how to build and load a minimal eBPF program into the kernel.

* [eBPF - From a Programmer's Perspective](https://www.researchgate.net/publication/349173667_eBPF_-_From_a_Programmer%27s_Perspective) - A short paper describing the fundamentals of eBPF and how to get started with writing eBPF programs.

* [Cloudflare's blog posts on eBPF](https://blog.cloudflare.com/tag/ebpf/) - Different blog posts about networking use cases and low-level aspects of eBPF.

* [Linux Extended BPF (eBPF) Tracing Tools](https://www.brendangregg.com/ebpf.html) - An in-depth collection of information around examples of performance analysis tools using eBPF. Contains also a section at the end of the page about other resources.

* [ebpf.io blog](https://ebpf.io/blog/) - Links to many community blogs posts.

### BPF Internals

* Daniel Borkmann has made several presentations and papers covering the internals of eBPF, in particular about its use with tc.

  * [eBPF and XDP walkthrough and recent (2017) updates](https://fosdem.org/2017/schedule/event/ebpf_xdp/)
  * [Advanced programmability and recent updates with tc's cls\_bpf](http://netdevconf.org/1.2/session.html?daniel-borkmann) - Details on eBPF, its use for tunneling and encapsulation, direct packet access, and more.
  * [cls\_bpf/eBPF updates since netdev 1.1](http://netdevconf.org/1.2/slides/oct5/07_tcws_daniel_borkmann_2016_tcws.pdf) - Part of [this tc workshop](http://netdevconf.org/1.2/session.html?jamal-tc-workshop).
  * [On getting tc classifier fully programmable with cls\_bpf](http://www.netdevconf.org/1.1/proceedings/slides/borkmann-tc-classifier-cls-bpf.pdf) - Introduction to eBPF, including several features (map management, tail calls, verifier). The full paper [is also available here](http://www.netdevconf.org/1.1/proceedings/papers/On-getting-tc-classifier-fully-programmable-with-cls-bpf.pdf).
  * [Linux tc and eBPF](https://archive.fosdem.org/2016/schedule/event/ebpf/attachments/slides/1159/export/events/attachments/ebpf/slides/1159/ebpf.pdf)

* [Linux Networking Explained](https://www.slideshare.net/slideshow/linux-networking-explained/65287988) - Linux networking internals, with a part about eBPF.

### Kernel Tracing

* [Full-system dynamic tracing on Linux using eBPF and bpftrace](https://www.joyfulbikeshedding.com/blog/2019-01-31-full-system-dynamic-tracing-on-linux-using-ebpf-and-bpftrace.html) - A detailed introduction to tracing with eBPF, from listing the available trace points to running bpftrace programs.
* [Meet-cute between eBPF and Kernel Tracing](https://www.slideshare.net/slideshow/meet-cutebetweenebpfandtracing/62446985) - Kprobes, uprobes, ftrace.
* [Linux Kernel Tracing](https://www.slideshare.net/slideshow/linux-kernel-tracing/65201573) - Systemtap, Kernelshark, trace-cmd, LTTng, perf-tool, ftrace, hist-trigger, perf, function tracer, tracepoint, kprobe/uprobe, and more.
* Brendan Gregg's blog, and in particular [Linux BPF Superpowers](http://www.brendangregg.com/blog/2016-03-05/linux-bpf-superpowers.html) article.

### XDP

* [eXpress Data Path (XDP)](https://github.com/iovisor/bpf-docs/raw/master/Express_Data_Path.pdf) ⭐ 1,017 | 🐛 3 | 📅 2022-09-20 - The first presentation about XDP.

* All XDP details in a technical paper: [The eXpress Data Path: Fast Programmable Packet Processing in the Operating System Kernel](https://github.com/tohojo/xdp-paper) ⭐ 154 | 🐛 2 | 🌐 CSS | 📅 2021-01-15, by Toke Høiland-Jørgensen, Jesper Dangaard Brouer, Daniel Borkmann, John Fastabend, Tom Herbert, David Ahern and David Miller, all being essential eBPF and XDP contributors.

* [The eXpress Data Path](https://blogs.igalia.com/dpino/2019/01/10/the-express-data-path/) - A very accessible introduction to XDP, providing sample code to show how to process packets.

* [Work-in-progress documentation for XDP](https://prototype-kernel.readthedocs.io/en/latest/networking/XDP/index.html)

* [BPF and XDP Reference Guide](http://docs.cilium.io/en/latest/bpf/) - Guide from the Cilium project.

* [XDP Project overview](https://www.iovisor.org/technology/xdp)

* [eXpress Data Path](https://www.slideshare.net/slideshow/express-data-path-linux-meetup-santa-clara-july-2016/64525115) - Contains some benchmark results obtained with the mlx4 driver.

* Jesper Dangaard Brouer has several sets of slides describing the internals of XDP:

  * [XDP − eXpress Data Path, Intro and future use-cases](http://people.netfilter.org/hawk/presentations/xdp2016/xdp_intro_and_use_cases_sep2016.pdf) - Linux Kernel's fight against DPDK. Future plans (as of this writing) for XDP and comparison with DPDK.
  * [Network Performance Workshop](http://netdevconf.org/1.2/session.html?jesper-performance-workshop) - Additional hints about XDP internals and expected evolution.
  * [XDP – eXpress Data Path, Used for DDoS protection](http://people.netfilter.org/hawk/presentations/OpenSourceDays2017/XDP_DDoS_protecting_osd2017.pdf) - Details and use cases about XDP, with benchmark results, and code snippets for benchmarking as well as for basic DDoS protection with eBPF/XDP (based on an IP blacklisting scheme).
  * [Memory vs. Networking, Provoking and fixing memory bottlenecks](http://people.netfilter.org/hawk/presentations/MM-summit2017/MM-summit2017-JesperBrouer.pdf) - Advanced details about current memory issues faced by XDP developers.
  * [XDP for the Rest of Us](http://netdevconf.org/2.1/session.html?gospodarek) - How to get started with eBPF and XDP for normal humans. Also summarized by Julia Evans on [her blog](http://jvns.ca/blog/2017/04/07/xdp-bpf-tutorial/).
  * [XDP now with REDIRECT](http://people.netfilter.org/hawk/presentations/LLC2018/XDP_LLC2018_redirect.pdf) - Update on XDP, and in particular on the redirect actions.

* [XDP workshop -- Introduction, experience, and future development (Video)](http://netdevconf.org/1.2/session.html?herbert-xdp-workshop)

* [High Speed Packet Filtering on Linux](https://cdn.shopify.com/s/files/1/0177/9886/files/phv2017-gbertin.pdf) - About packet filtering on Linux, DDoS protection, packet processing in the kernel, kernel bypass, XDP and eBPF.

* [How to drop 10 million packets per second](https://blog.cloudflare.com/how-to-drop-10-million-packets/) - Cloudflare's blog post talking about their move to using XDP for packet filtering.

### AF\_XDP

* [AF\_XDP](https://www.kernel.org/doc/html/latest/networking/af_xdp.html) - Kernel documentation on the AF\_XDP address family.
* [Fast Packet Processing in Linux with AF\_XDP](https://archive.fosdem.org/2018/schedule/event/af_xdp/)

### bpfilter

* [Why is the kernel community replacing iptables with BPF?](https://cilium.io/blog/2018/04/17/why-is-the-kernel-community-replacing-iptables/) - A blog post by Cilium on the motivations behind eBPF and bpfilter, with a couple examples and links to other projects using eBPF and bpfilter.
* [bpfilter: Linux firewall with eBPF sauce](https://qmo.fr/docs/talk_20180316_frnog_bpfilter.pdf) - Slides from a talk by Quentin Monnet with a background on eBPF and comparing bpfilter to iptables.

### BTF

* [BPF Type Format (BTF)](https://www.kernel.org/doc/html/latest/bpf/btf.html) - Kernel documentation about BTF, explaining how to use it.
* [Enhancing the Linux kernel with BTF type information](https://facebookmicrosites.github.io/bpf/blog/2018/11/14/btf-enhancement.html) - A description of the work done with BTF to provide debugging information for BPF programs.
* [What is BTF (BPF Type Format)](https://cloudchirp.substack.com/p/what-is-btf-bpf-type-format) - A community-authored newsletter enriched with useful code illustrations and hands-on examples.

### cBPF

* [The BSD Packet Filter: A New Architecture for User-level Packet Capture](http://www.tcpdump.org/papers/bpf-usenix93.pdf) - The original paper about (classic) BPF.
* [The FreeBSD manual page about BPF](https://www.freebsd.org/cgi/man.cgi?query=bpf\&sektion=4)
* [Linux' packet mmap(2), BPF, and Netsniff-NG](http://borkmann.ch/talks/2013_devconf.pdf)
* [tc and cls bpf: lightweight packet classifying with BPF](http://borkmann.ch/talks/2014_devconf.pdf)
* [Introducing Cloudflare's BPF Tools](https://blog.cloudflare.com/introducing-the-bpf-tools/) - Usage of BPF bytecode with the `xt_bpf` module for iptables.
* [Libpcap filters syntax](http://biot.com/capstats/bpf.html)

### Hardware Offload

* [hBPF - eBPF in hardware](https://github.com/rprinz08/hBPF) ⭐ 434 | 🐛 0 | 🌐 Python | 📅 2023-01-27 - An eBPF CPU written for FPGAs.
* [OpenCSD eBPF SSD offloading](https://github.com/Dantali0n/qemu-csd) ⭐ 69 | 🐛 0 | 🌐 C++ | 📅 2023-11-01 - Computational Storage simulation (QEMU) platform with FUSE LFS filesystem for Zoned Namespaces NVMe SSDs using uBPF for compute kernel offloading, all in userspace.
* [eBPF/XDP hardware offload to SmartNICs](http://netdevconf.org/1.2/session.html?jakub-kicinski) - Hardware offload for eBPF with TC or XDP (Linux kernel 4.9+), introduced by Netronome.
* [Comprehensive XDP offload---Handling the edge cases](https://www.netdevconf.org/2.2/session.html?viljoen-xdpoffload-talk) - An update on the topic above.
* [Delilah: eBPF-offload on Computational Storage](https://dl.acm.org/doi/pdf/10.1145/3592980.3595319) - Delilah is a Computational Storage Processor (CSP) built for eBPF offload to storage devices.

## Tutorials

* [bcc Reference Guide](https://github.com/iovisor/bcc/blob/master/docs/reference_guide.md) ⭐ 22,650 | 🐛 1,073 | 🌐 C | 📅 2026-08-27 - Many incremental steps to start using bcc and eBPF, mostly centered on tracing and monitoring.
* [bcc Python Developer Tutorial](https://github.com/iovisor/bcc/blob/master/docs/tutorial_bcc_python_developer.md) ⭐ 22,650 | 🐛 1,073 | 🌐 C | 📅 2026-08-27 - Comes with bcc, but targets the Python bits across seventeen "lessons".
* [XDP Hands-On Tutorial](https://github.com/xdp-project/xdp-tutorial) ⭐ 2,964 | 🐛 170 | 🌐 C | 📅 2026-05-08 - A progressive (three levels of difficulty) tutorial to learn how to process packets with XDP.
* [Linux Tracing Workshops Materials](https://github.com/goldshtn/linux-tracing-workshop) ⭐ 1,322 | 🐛 7 | 🌐 HTML | 📅 2020-06-19 - Involves the use of several BPF tools for tracing.
* [eBPF Party](https://ebpf.party/) - Browser-based playground to learn, write, compile, and run eBPF programs.
* [Building BPF applications with libbpf-bootstrap](https://nakryiko.com/posts/libbpf-bootstrap/) - Helps generate minimal or advanced templates to bootstrap your own applications (kernel side and user space management for maps and programs) with features like CO-RE, global variables, and ring buffer.
* [How I ended up writing opensnoop in pure C using eBPF](https://bolinfest.github.io/opensnoop-native/) - A thorough walk-through of how to write eBPF programs, first using only bpf() syscall, and then libbpf library, with reproducible code examples.
* [Tracing a packet journey using Linux tracepoints, perf and eBPF](https://blog.yadutaf.fr/2017/07/28/tracing-a-packet-journey-using-linux-tracepoints-perf-ebpf/) - Troubleshooting ping requests and replies with perf and bcc programs.
* [Open NFP platform](https://open-nfp.org/dataplanes-ebpf/technical-papers/) - Operated by Netronome: some tutorials for network-related eBPF use cases, including an eBPF Offload Starting Guide.
* [XDP for the Rest of Us](http://netdevconf.org/2.1/session.html?gospodarek) - First edition of a workshop to get started with XDP.
* [XDP for the Rest of Us](https://www.netdevconf.org/2.2/session.html?gospodarek-xdp-workshop) - Second edition, with new contents.
* [All your tracing are belong to BPF](https://blog.trailofbits.com/2021/11/09/all-your-tracing-are-belong-to-bpf/) - A step-by-step walkthrough to integrate tracing capabilities in your C++ applications with the LLVM libraries.
* [Firewalling with BPF/XDP: Examples and Deep Dive](https://arthurchiao.art/blog/firewalling-with-bpf-xdp/) - A simple guide to build basic firewalls with TC and XDP.
* [A Deep Dive into eBPF: Writing an Efficient DNS Monitoring.](https://medium.com/@nurkholish.halim/a-deep-dive-into-ebpf-writing-an-efficient-dns-monitoring-2c9dea92abdf) - A detailed explanation of methods used to capture DNS requests at the socket filter layer.
* [eBPF Developer Tutorial - Learn eBPF by examples](https://eunomia.dev/tutorials/) - Start with eBPF basics and progress to advanced topics using 20+ hands-on tutorials and examples. Covers performance, networking, and security with libbpf and CO-RE. Available in Chinese and English.
* [Catch Performance Regressions in eBPF](https://bencher.dev/docs/explanation/talks/#linuxcon-2023-12-may-23) - A step-by-step guide to benchmarking both the client and kernel eBPF code written in Rust.
* [Loops and Iterators in eBPF](https://cloudchirp.substack.com/p/loops-and-iterators-in-ebpf) - Newsletter about all the ways to loop and iterate in eBPF.
* [What Insights Can eBPF Provide into Real-Time SSL/TLS Encrypted Traffic and How?](https://cloudchirp.substack.com/p/what-insights-can-ebpf-provide-into) - A step-by-step guide how eBPF can observe encrypted network traffic.
* [Can eBPF Detect Redis Message Patterns Before They Become Problems?](https://cloudchirp.substack.com/p/can-ebpf-detect-redis-message-patterns) - A step-by-step guide how eBPF can observe Redis communication between client and server.
* [Transparent Proxy Implementation using eBPF and Go](https://cloudchirp.substack.com/p/transparent-proxy-implementation) - A step-by-step guide on how to implement a transparent proxy using eBPF.
* [eBPF-Powered Load Balancing](https://cloudchirp.substack.com/p/ebpf-powered-load-balancing-for-so_reuseport) - Learn how eBPF can infer custom load-balancing for services listening on the same port, through the SO\_REUSEPORT TCP option.
* [Unit Testing eBPF Programs](https://ebpfchirp.substack.com/p/unit-testing-ebpf-programs) - Learn how you can unit test your eBPF programs using libbpf.
* [Accelerating Local Socket Communication using eBPF](https://cloudchirp.substack.com/p/optimizing-local-socket-communication) - Learn how eBPF can speed-up local socket communication up to 30%.
* [Writing a basic continuous profiler](https://blog.maxgio.me/posts/unleashing-power-frame-pointers-writing-simple-continuous-profiler/) - A step-by-step guide to write an appliation continuous profiler leveraging the eBPF instrumentation, with a complete project as a reference.
* [Inspektor Gadget - Hello world gadget](https://inspektor-gadget.io/docs/latest/gadget-devel/hello-world-gadget) - An introductory guide to writing image-based eBPF gadgets and sharing them via OCI registries.
* [Inspektor Gadget - Hello world gadget with Wasm](https://inspektor-gadget.io/docs/latest/gadget-devel/hello-world-gadget-wasm) - An introductory guide to writing image-based eBPF gadgets and performing post-processing with WASM.
* [ebpf.io labs](https://ebpf.io/labs/) - List of community developed labs.

## Examples

* [bcc/examples](https://github.com/iovisor/bcc/tree/master/examples) ⭐ 22,650 | 🐛 1,073 | 🌐 C | 📅 2026-08-27 - Examples coming along with the bcc tools, mostly about tracing.
* [bcc/tools](https://github.com/iovisor/bcc/tree/master/tools) ⭐ 22,650 | 🐛 1,073 | 🌐 C | 📅 2026-08-27 - These tools themselves can be seen as example use cases for BPF programs, mostly for tracing and monitoring. bcc tools have been packaged for some Linux distributions.
* [redbpf examples](https://github.com/foniod/redbpf/tree/main/examples) ⚠️ Archived - Example programs for using RedBPF to write eBPF programs in Rust.
* [prototype-kernel/kernel/samples/bpf](https://github.com/netoptimizer/prototype-kernel/tree/master/kernel/samples/bpf) ⭐ 316 | 🐛 13 | 🌐 C | 📅 2025-01-16 - Jesper Dangaard Brouer's prototype-kernel repository contains some additional examples that can be compiled outside of kernel infrastructure.
* [Netronome sample network applications](https://github.com/Netronome/bpf-samples/) ⭐ 107 | 🐛 6 | 🌐 C | 📅 2020-04-06 - Provides basic but complete examples of eBPF applications also compatible with hardware offload.
* [ebpf-samples](https://github.com/vbpf/ebpf-samples) ⭐ 93 | 🐛 0 | 🌐 C | 📅 2026-07-03 - A collection of compiled (as ELF object files) samples gathered from several projects, primarily intended to serve as test cases for user space verifiers.
* [XDP/TC-eBPF example](https://github.com/netfoundry/zfw) ⭐ 84 | 🐛 0 | 🌐 C | 📅 2025-08-05 - Program that uses XDP/TC-eBPF to provide statefull firewalling and socket redirection.
* [MPLSinIP sample](https://github.com/fzakaria/eBPF-mpls-encap-decap) ⭐ 58 | 🐛 0 | 🌐 C | 📅 2019-10-18 - A heavily commented sample demonstrating how to encapsulate and decapsulate MPLS within IP. The code is commented for those new to BPF development.
* [ebpf-kill-example](https://github.com/niclashedam/ebpf-kill-example) ⭐ 23 | 🐛 1 | 🌐 C | 📅 2026-07-13 - A fully documented and tested example of an eBPF probe that logs all force-kills and prints them out in user-space.
* [linux/samples/bpf/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/samples/bpf) - In the kernel tree: some sample eBPF programs.
* [linux/tools/testing/selftests/bpf](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/tools/testing/selftests/bpf) - In the kernel tree: Linux BPF selftests, with many eBPF programs.
* [iproute2/examples/bpf/](https://git.kernel.org/pub/scm/network/iproute2/iproute2-next.git/tree/examples/bpf) - Some networking programs to attach to the TC interface.

## eBPF Workflow: Tools and Utilities

### bcc

* [bcc](https://github.com/iovisor/bcc/) ⭐ 22,650 | 🐛 1,073 | 🌐 C | 📅 2026-08-27 - Framework and set of tools - One way to handle BPF programs, in particular for tracing and monitoring. Also includes some utilities that may help inspect maps or programs on the system.
* [Lua front-end for BCC](https://github.com/iovisor/bcc/tree/master/src/lua) ⭐ 22,650 | 🐛 1,073 | 🌐 C | 📅 2026-08-27 - Another alternative to C, and even to most of the Python code used in bcc.

### iproute2

* [iproute2](https://git.kernel.org/pub/scm/network/iproute2/iproute2.git) - Package containing tools for network management on Linux. In particular, it contains `tc`, used to manage eBPF filters and actions, and `ip`, used to manage XDP programs. Most of the code related to BPF is in lib/bpf.c.
* [iproute2-next](https://git.kernel.org/pub/scm/network/iproute2/iproute2-next.git) - The development tree, synchronised with net-next.

### LLVM

* [LLVM](https://llvm.org/) - Contains several tools used in eBPF workflows. Snapshots of the latest versions for Ubuntu/Debian can be retrieved from [here](http://apt.llvm.org/).

  * clang is used to compile C to eBPF object file under the ELF format (clang v3.7.1+). The BPF backend was added with [this commit](https://reviews.llvm.org/D6494).
  * llvm-objdump is used to dump the content of an object file in human-readable format, possibly with the initial C source code (llvm-objdump v4.0+).
  * llvm-mc is used to compile from LLVM intermediate representation to eBPF object file, so that one can compile from C to eBPF assembly, tinker with assembly, then compile to ELF file.

### libbpf

* [libbpf](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git/tree/tools/lib/bpf) - A C library used for handling BPF objects (programs and maps), and manipulating ELF object files containing them. It is shipped with the kernel and [mirrored on GitHub](https://github.com/libbpf/libbpf) ⭐ 2,753 | 🐛 35 | 🌐 C | 📅 2026-07-30.
* [libbpf-bootstrap](https://github.com/libbpf/libbpf-bootstrap) ⭐ 1,519 | 🐛 18 | 🌐 CMake | 📅 2026-08-31 - Scaffolding for BPF application development with libbpf and BPF CO-RE.

### Go libraries

* [cilium/ebpf](https://github.com/cilium/ebpf) ⭐ 7,938 | 🐛 24 | 🌐 Go | 📅 2026-09-01 - Pure-Go library to read, modify and load eBPF programs and attach them to various hooks in the Linux kernel.
* [libbpfgo](https://github.com/aquasecurity/libbpfgo) ⭐ 849 | 🐛 35 | 🌐 Go | 📅 2026-09-01 - eBPF library for Go, powered by libbpf.

### Aya

* [aya](https://github.com/aya-rs/aya) ⭐ 4,789 | 🐛 210 | 🌐 Rust | 📅 2026-09-01 - A pure Rust library for writing, loading, and managing eBPF objects, with a focus on developer experience and operability. It supports writing eBPF programs in Rust and distributing library code over crates.io to share it between eBPF programs. Aya does not depend on libbpf.
* [aya-template](https://github.com/aya-rs/aya-template) ⭐ 140 | 🐛 6 | 🌐 Rust | 📅 2026-08-31 - Templates for writing BPF applications in Aya that can be used with [`cargo generate`](https://github.com/cargo-generate/cargo-generate) ⭐ 2,485 | 🐛 27 | 🌐 Rust | 📅 2026-08-31.

### zbpf

* [zbpf](https://github.com/tw4452852/zbpf) ⭐ 277 | 🐛 5 | 🌐 Zig | 📅 2026-04-19 - A pure Zig framework for writing cross platform eBPF programs, powered by libbpf and Zig toolchain.

### eunomia-bpf

* [eunomia-bpf](https://github.com/eunomia-bpf/eunomia-bpf) ⭐ 898 | 🐛 15 | 🌐 Rust | 📅 2026-08-09 - A compilation framework and runtime library to build, distribute, dynamically load, and run CO-RE eBPF applications in multiple languages and WebAssembly. It supports writing eBPF kernel code only (to build simple CO-RE libbpf eBPF applications), writing the kernel part in both BCC and libbpf styles, and writing userspace in multiple languages in a WASM module and distributing it with simple JSON data or WASM OCI images. The runtime is based on libbpf only and provides CO-RE to BCC-style eBPF programs without depending on the LLVM library.

### bpftool and Other Tools from the Kernel Tree

* [bpftool](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpftool) - Also some other tools in the kernel tree, under [linux/tools/net/](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/tools/net?h=v4.14) for versions earlier than 4.15, or [linux/tools/bpf/](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git/tree/tools/bpf) after that:

  * [`bpftool`](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpftool) - A generic utility that can be used to interact with eBPF programs and maps from userspace, for example to show, dump, load, disassemble, pin programs, or to show, create, pin, update, delete maps, or to attach and detach programs to cgroups.
  * [`bpf_asm`](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpf_asm.c) - A minimal cBPF assembler.
  * [`bpf_dbg`](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpf_dbg.c) - A small debugger for cBPF programs.
  * [`bpf_jit_disasm`](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpf_jit_disasm.c) - A disassembler for both BPF flavors and could be highly useful for JIT debugging.

### User Space eBPF

* [rbpf](https://github.com/qmonnet/rbpf) ⭐ 1,126 | 🐛 17 | 🌐 Rust | 📅 2026-06-03 - Written in Rust. Interpreter for Linux, macOS and Windows, and JIT-compiler for x86\_64 under Linux.
* [uBPF](https://github.com/iovisor/ubpf/) ⭐ 988 | 🐛 18 | 🌐 C | 📅 2026-08-08 - Written in C. Contains an interpreter, a JIT compiler for x86\_64 architecture, an assembler and a disassembler.
* [PREVAIL](https://github.com/vbpf/ebpf-verifier) ⭐ 469 | 🐛 42 | 🌐 C++ | 📅 2026-08-29 - A user space verifier for eBPF [using an abstract interpretation layer](https://elazarg.github.io/pldi19main-final.pdf), with support for loops.
* [A generic implementation](https://github.com/YutaroHayakawa/generic-ebpf) ⭐ 154 | 🐛 2 | 🌐 C | 📅 2021-05-28 - With support for FreeBSD kernel, FreeBSD user space, Linux kernel, Linux user space and macOS user space. Used for the [VALE software switch](https://www.unix.com/man-page/freebsd/4/vale/)'s [BPF extension module](https://github.com/YutaroHayakawa/vale-bpf) ⭐ 33 | 🐛 0 | 🌐 C | 📅 2019-11-06.
* [wachy](https://rubrikinc.github.io/wachy/) - A tracing profiler that aims to make eBPF uprobe-based debugging easier to use. This is done by displaying traces in a UI next to the source code and allowing interactive drilldown analysis.

### eBPF on Other Platforms

* [eBPF for Windows](https://github.com/microsoft/ebpf-for-windows) ⭐ 3,555 | 🐛 326 | 🌐 C | 📅 2026-08-31 - This project is a work-in-progress that allows using existing eBPF toolchains and APIs familiar in the Linux ecosystem to be used on top of Windows.

### Testing in Virtual Environments

* [bcc in a Docker container](https://github.com/zlim/bcc-docker) ⭐ 45 | 🐛 4 | 🌐 Makefile | 📅 2020-07-23
* [bpfcompat](https://github.com/Kernel-Guard/bpfcompat) ⭐ 18 | 🐛 8 | 🌐 Go | 📅 2026-08-31 - Boots real Linux kernels in disposable QEMU/KVM VMs to load- and attach-validate compiled eBPF objects across a multi-distro, multi-architecture kernel matrix, classifying failures (missing BTF, unsupported map/program type, CO-RE relocations); runs as a CI gate and GitHub Action.

## Projects Related to eBPF

### Networking

* [Cilium](https://cilium.io/) project ([GitHub repository](https://github.com/cilium/cilium) ⭐ 25,037 | 🐛 1,080 | 🌐 Go | 📅 2026-09-01) is a technology relying on eBPF and XDP to provide "fast in-kernel networking and security policy enforcement for containers based on eBPF programs generated on the fly". Many presentations available (with overlap):

  * [Cilium: Networking & Security for Containers with BPF & XDP](https://www.slideshare.net/slideshow/clium-container-networking-with-bpf-xdp/68194576) - Also featuring a load balancer use case
  * [Cilium: Networking & Security for Containers with BPF & XDP](https://www.slideshare.net/slideshow/cilium-bpf-xdp-for-containers-66969823/66969823) - [video](https://www.youtube.com/watch?v=TnJF7ht3ZYc\&list=PLkA60AVN3hh8oPas3cq2VA9xB7WazcIgs)
  * [Cilium: Fast IPv6 container Networking with BPF and XDP](https://www.slideshare.net/slideshow/cilium-fast-ipv6-container-networking-with-bpf-and-xdp/65332240)
  * [Cilium: BPF & XDP for containers](https://fosdem.org/2017/schedule/event/cilium/)
  * [OvS Orbit episode (#4)](https://ovsorbit.benpfaff.org/) - Interview of Thomas Graf by Ben Pfaff.
  * [A generic introduction to Cilium](https://opensource.googleblog.com/2016/11/cilium-networking-and-security.html)
  * [A podcast interviewing Thomas Graf](https://blog.ipspace.net/2016/10/fast-linux-packet-forwarding-with/) - Ivan Pepelnjak interviewing Thomas, October 2016, on eBPF, P4, XDP and Cilium.

* [ApFree WiFiDog](https://github.com/liudf0716/apfree-wifidog) ⭐ 935 | 🐛 2 | 🌐 C | 📅 2026-08-27 - A high performance and lightweight captive portal solution for wireless networks. It leverages eBPF for traffic control and deep packet inspection capabilities, with plans to gradually replace nftables firewall functionality with eBPF-based solutions.

* [merbridge](https://github.com/merbridge/merbridge/) ⭐ 808 | 🐛 36 | 🌐 Go | 📅 2025-05-19 - Use eBPF to speed up your Service Mesh. Merbridge replaces iptables rules with eBPF to intercept traffic. It also combines msg\_redirect to reduce latency with a shortened datapath between sidecars and services.

* [ipx\_wrap](https://github.com/twisted-pear/ipx_wrap) ⭐ 10 | 🐛 0 | 🌐 C | 📅 2026-08-31 - A proof-of-concept IPX implementation for Linux using eBPF.

* P4 has some interactions with eBPF:

  * [P4\_16 backend for eBPF](https://github.com/p4lang/p4c/blob/master/backends/ebpf/README.md) ⭐ 836 | 🐛 470 | 🌐 C++ | 📅 2026-09-01
  * [OvS Orbit episode (#11), called P4 on the Edge](https://ovsorbit.org/#e11) - Related to the former item. Audio interview of John Fastabend by Ben Pfaff, one of the core maintainers of Open vSwitch.

* [Katran](https://code.fb.com/open-source/open-sourcing-katran-a-scalable-network-load-balancer/) - A layer 4 load-balancer based on XDP, open-sourced by Facebook.

* [XDP in practice: integrating XDP in our DDoS mitigation pipeline](http://netdevconf.org/2.1/session.html?bertin) - Protection against DDoS with XDP at Cloudflare.

* [Droplet: DDoS countermeasures powered by BPF + XDP](http://netdevconf.org/2.1/session.html?zhou) - Protection against DDoS with XDP at Facebook.

* [DPDK has a poll-mode driver (PMD) based on AF\_XDP](https://dpdkuserspace2018.sched.com/event/G45Z/dpdk-pmd-for-afxdp)

* [CETH for XDP](http://www.slideshare.net/IOVisor/ceth-for-xdp-linux-meetup-santa-clara-july-2016) - Common Ethernet Driver Framework for faster network I/O, a technology initiated by Mellanox.

* Suricata, an open source intrusion detection system, relies on eBPF components for its "capture bypass" features:

  * [SEPTun-Mark-II](https://github.com/pevma/SEPTun-Mark-II) ⭐ 121 | 🐛 2 | 🌐 Makefile | 📅 2018-04-17 - Extreme Performance Tuning guide - Mark II.
  * ["eBPF and XDP" section of Suricata documentation](http://suricata.readthedocs.io/en/latest/capture-hardware/ebpf-xdp.html?highlight=XDP#ebpf-and-xdp)
  * [A blog post introducing the "capture bypass" feature](https://www.stamus-networks.com/blog/2016/09/28/suricata-bypass-feature)
  * [The adventures of a Suricate in eBPF land](http://netdevconf.org/1.2/slides/oct6/10_suricata_ebpf.pdf)
  * [eBPF and XDP seen from the eyes of a meerkat](https://www.slideshare.net/ennael/kernel-recipes-2017-ebpf-and-xdp-eric-leblond)

* [Project Calico](https://projectcalico.docs.tigera.io/about/about-calico) - Calico is an open source networking and network security solution for containers, virtual machines, and native host-based workloads. Calico's eBPF data plane delivers a low latency, high throughput data plane with a rich network security policy model.
  * [Enabling eBPF data plane with Calico](https://projectcalico.docs.tigera.io/maintenance/ebpf/enabling-bpf)

* [PcapPlusPlus](https://pcapplusplus.github.io/) - An open-source C++ library for capturing, parsing and crafting network packets. It features a C++ interface for creating AF\_XDP sockets, making it easy to [send and receive packets through them](https://pcapplusplus.github.io/docs/next/features#af_xdp-support-beta).

### Observability

* [Coroot](https://github.com/coroot/coroot) ⭐ 7,901 | 🐛 120 | 🌐 Go | 📅 2026-08-27 - Coroot is an open-source APM and observability tool, a DataDog and NewRelic alternative.
* [pixie](https://github.com/pixie-io/pixie) ⭐ 6,527 | 🐛 395 | 🌐 C++ | 📅 2026-07-30 - Observability for Kubernetes using eBPF. Features include protocol tracing, application profiling, and support for distributed bpftrace deployments.
* [kyanos](https://github.com/hengyoush/kyanos) ⭐ 5,070 | 🐛 32 | 🌐 C | 📅 2026-08-29 - Kyanos is an eBPF-based network issue analysis tool that enables you to capture network requests, such as HTTP, Redis, and MySQL requests.
* [Hubble](https://github.com/cilium/hubble) ⭐ 4,319 | 🐛 44 | 🌐 Makefile | 📅 2026-09-01 - Network, service and security observability for Kubernetes using eBPF.
* [DeepFlow](https://github.com/deepflowio/deepflow) ⭐ 4,251 | 🐛 268 | 🌐 Go | 📅 2026-08-31 - Instant observability for cloud-native and AI applications based on eBPF.
* [Caretta](https://github.com/groundcover-com/caretta) ⭐ 2,058 | 🐛 18 | 🌐 Go | 📅 2025-03-17 - Instant Kubernetes service dependency map generated by eBPF, right to a Grafana instance.
* [InKeV: In-Kernel Distributed Network Virtualization for DCN](https://github.com/iovisor/bpf-docs/blob/master/university/sigcomm-ccr-InKev-2016.pdf) ⭐ 1,017 | 🐛 3 | 📅 2022-09-20
* [parca-agent](https://github.com/parca-dev/parca-agent) ⭐ 743 | 🐛 179 | 🌐 Go | 📅 2026-09-01 - eBPF based always-on continuous profiler for analysis of CPU and memory usage, down to the line number and throughout time.
* [SkyWalking Rover](https://github.com/apache/skywalking-rover) ⭐ 237 | 🐛 3 | 🌐 Go | 📅 2026-08-28 - [Apache SkyWalking](https://skywalking.apache.org/) is an open-source Application Performance Monitoring (APM) platform specially designed for distributed systems with microservices, cloud-native and container-based (Kubernetes) architectures. SkyWalking Rover is an eBPF-based profiler and metrics collector for C, C++, Golang, and Rust applications.
* [rbperf](https://github.com/javierhonduco/rbperf) ⭐ 124 | 🐛 8 | 🌐 Rust | 📅 2024-04-21 - Sampling profiler and tracer for Ruby.
* [kpod-metrics](https://github.com/pjs7678/kpod-metrics) ⭐ 13 | 🐛 4 | 🌐 C | 📅 2026-08-01 - eBPF-based pod-level kernel metrics collector for Kubernetes. Exports per-pod CPU, network, memory, syscall, disk I/O, and L7 protocol metrics to Prometheus. BPF programs are defined using a [Kotlin DSL](https://github.com/pjs7678/kotlin-ebpf-dsl) ⭐ 0 | 🐛 0 | 🌐 Kotlin | 📅 2026-03-09 instead of C.
* [eTraceGen](https://github.com/bhanuprakasheagala/eTraceGen-eBPFEventTelemetryEngine) ⭐ 4 | 🐛 0 | 🌐 C++ | 📅 2026-07-26 - eTraceGen is a Linux telemetry engine built with eBPF and Modern C++ that captures kernel-level events for processes, files, system calls, and network with a modular pipeline for decoding, enrichment, filtering, and JSON output.
* [rstat](https://github.com/overyonder/rstat) ⭐ 3 | 🐛 1 | 🌐 Rust | 📅 2026-08-26 - Sub-millisecond system monitoring using eBPF tracepoints on sched\_switch, sched\_process\_exit, and sched\_process\_free, with zero heap allocations in steady state.
* [DEEP-mon](https://www.slideshare.net/slideshow/deepmon-dynamic-and-energy-efficient-power-monitoring-for-containerbased-infrastructures/97832653) - Helps with measuring power consumption for servers and uses eBPF programs for in-kernel aggregation of data.
* [Ingero](https://github.com/ingero-io/ingero) - eBPF-based GPU causal observability agent. Traces CUDA Runtime and Driver APIs via uprobes and host kernel events via tracepoints to build causal chains explaining GPU latency, with <2% overhead.

### Security

* [Tetragon](https://github.com/cilium/tetragon) ⭐ 4,976 | 🐛 269 | 🌐 C | 📅 2026-09-01 - Kubernetes-aware, eBPF-based security observability and runtime enforcement.
* [Tracee](https://github.com/aquasecurity/tracee) ⭐ 4,598 | 🐛 123 | 🌐 Go | 📅 2026-09-01 - A runtime security and forensics tool for Linux which uses eBPF technology to trace the system and applications at runtime, and analyze collected events to detect suspicious behavioral patterns.
* [Sysmon for Linux](https://github.com/Sysinternals/SysmonForLinux) ⭐ 2,154 | 🐛 42 | 🌐 C | 📅 2026-07-13 - A security monitoring tool. It depends on [SysinternalsEBPF](https://github.com/Sysinternals/SysinternalsEBPF) ⭐ 289 | 🐛 16 | 🌐 C | 📅 2026-05-07.
* [owLSM](https://github.com/Cybereason-Public/owLSM) ⭐ 281 | 🐛 2 | 🌐 C | 📅 2026-08-22 - Open source agent that implements a stateful Sigma rules engine focused on monitoring and prevention using eBPF LSM.
* [harpoon](https://github.com/alegrey91/harpoon) ⭐ 178 | 🐛 8 | 🌐 C | 📅 2026-02-23 - Trace syscalls from user-space functions, by using eBPF.
* [bpflock - Lock Linux machines](https://github.com/linux-lock/bpflock) ⭐ 157 | 🐛 3 | 🌐 C | 📅 2022-02-16 - An eBPF driven security tool for locking and auditing Linux machines.
* [redcanary-ebpf-sensor](https://github.com/redcanaryco/redcanary-ebpf-sensor) ⭐ 116 | 🐛 0 | 🌐 C | 📅 2026-06-26 - A set of BPF programs that gather security relevant event data from the Linux kernel. The BPF programs are combined into a single ELF file from which individual probes can be selectively loaded, depending on the running operating system and kernel version.
* [BPFJailer](https://github.com/gen0sec/bpfjailer) ⭐ 59 | 🐛 1 | 🌐 C | 📅 2026-08-26 - BpfJailer is an eBPF-based process jailing system that provides mandatory access control (MAC) for Linux.
* [Bombini](https://github.com/bombinisecurity/bombini) ⭐ 58 | 🐛 16 | 🌐 Rust | 📅 2026-08-31 - An eBPF-based security agent written entirely in Rust using the [Aya](https://github.com/aya-rs/aya) ⭐ 4,789 | 🐛 210 | 🌐 Rust | 📅 2026-09-01 library and built on LSM (Linux Security Module) BPF hooks.
* [Falco](https://falco.org/) - A cloud-native runtime security project used as a Kubernetes threat detection engine.
* [Red Canary Linux Agent](https://redcanary.com/blog/ebpf-for-security) - Red Canary has started to incorporate eBPF to their Linux security sensor.
* [Synapse](https://github.com/gen0sec/synapse) - Extended detection and response (XDR) with eBPF-powered firewall and proxy, to protect your Linux servers.
* [Inner Warden](https://github.com/InnerWarden/innerwarden) - A self-defending security agent for Linux and macOS that uses eBPF with 22 kernel hooks (tracepoints, kprobes, LSM, XDP) via the Aya library for real-time threat detection, automated response, and AI-powered triage.

### Linux Scheduler

* [scx](https://github.com/sched-ext/scx) ⭐ 2,141 | 🐛 79 | 🌐 C | 📅 2026-09-01 - sched\_ext schedulers and tools.
* [Gthulhu](https://github.com/Gthulhu/Gthulhu) ⭐ 402 | 🐛 5 | 🌐 Go | 📅 2026-09-01 - Gthulhu optimizes cloud-native workloads using the Linux Scheduler Extension for different application scenarios.

### Tools

* [oryx](https://github.com/pythops/oryx) ⭐ 2,572 | 🐛 5 | 🌐 Rust | 📅 2026-09-01 - A TUI for sniffing network traffic using eBPF on Linux.
* [kubectl trace](https://github.com/iovisor/kubectl-trace) ⭐ 2,186 | 🐛 49 | 🌐 Go | 📅 2026-04-16 - A kubectl plug-in for executing bpftrace programs in a Kubernetes cluster.
* [redbpf](https://github.com/foniod/redbpf) ⚠️ Archived - Tooling and framework to write eBPF code in Rust efficiently.
* [ptcpdump](https://github.com/mozillazg/ptcpdump) ⭐ 1,267 | 🐛 29 | 🌐 C | 📅 2026-09-01 - A process-aware, eBPF-based tcpdump-like tool.
* [bpfman](https://github.com/bpfman/bpfman) ⭐ 762 | 🐛 17 | 🌐 Go | 📅 2026-08-31 - An eBPF Manager for Linux and Kubernetes. Includes a built-in program loader that supports program cooperation for XDP and TC programs, as well as deployment of eBPF programs from OCI images.
* [AgentSight](https://github.com/eunomia-bpf/AgentSight) ⭐ 635 | 🐛 25 | 🌐 C | 📅 2026-08-31 - Zero-instrumentation eBPF observability for LLM and coding agents, capturing syscall-level traces (file, network, process) without modifying the agent.
* [bpfd](https://github.com/genuinetools/bpfd) ⭐ 483 | 🐛 5 | 🌐 Go | 📅 2021-05-07 - Framework for running BPF programs with rules on Linux as a daemon. Container aware.
* [adeb](https://github.com/joelagnel/adeb) ⚠️ Archived - A Linux shell environment for using tracing tools on Android with BPFd.
* [upf-bpf](https://github.com/navarrothiago/upf-bpf) ⭐ 217 | 🐛 17 | 🌐 C++ | 📅 2024-09-28 - An in-kernel solution based on XDP for 5G UPF.
* [GhostScope](https://github.com/swananan/ghostscope) ⭐ 188 | 🐛 5 | 🌐 Rust | 📅 2026-09-01 - A DWARF-aware eBPF tracer for source-level userspace tracing, with an interactive TUI and a scriptable CLI.
* [BPFd](https://github.com/joelagnel/bpfd) ⚠️ Archived - A distinct BPF daemon, trying to leverage the flexibility of the bcc tools to trace and debug remote targets, and in particular devices running with Android.
* [ActPlane](https://github.com/eunomia-bpf/ActPlane) ⭐ 95 | 🐛 1 | 🌐 C | 📅 2026-08-31 - OS-level agent harness that compiles a policy DSL to an in-kernel eBPF engine for labeled information-flow control at the syscall boundary, enforcing constraints across any tool or subprocess.
* [ebpf-explorer](https://github.com/ebpfdev/explorer) ⭐ 93 | 🐛 9 | 🌐 Dockerfile | 📅 2023-06-18 - A web interface to explore system's maps and programs.
* [ebpfmon](https://github.com/redcanaryco/ebpfmon) ⭐ 90 | 🐛 1 | 🌐 Go | 📅 2025-12-05 - A TUI (terminal user interface) application for real time monitoring of eBPF programs.
* [greggd](https://github.com/olcf/greggd) ⭐ 6 | 🐛 4 | 🌐 Go | 📅 2025-03-20 - System daemon to compile and load eBPF programs into the kernel, and forward program output to socket for metric aggregation.
* [ply](https://wkz.github.io/ply/) - A small but flexible open source dynamic tracer for Linux, with features similar to the bcc tools, but with a simpler language inspired by awk and DTrace.
* [bpftrace](https://bpftrace.org/) - A tool for tracing with its own high-level tracing language. It is flexible enough to be envisioned as a Linux replacement for DTrace and SystemTap.
  * [bpftrace Cheat Sheet](https://www.brendangregg.com/BPF/bpftrace-cheat-sheet.html) - Summary and cheat sheet for programming in bpftrace. Contains information about syntax, probe types, variables and functions.
* [inspektor-gadget](https://inspektor-gadget.io) - A collection tools and framework for data collection and system inspection on Kubernetes clusters and Linux hosts using eBPF.
* [FUSE](https://events.linuxfoundation.org/wp-content/uploads/2017/11/When-eBPF-Meets-FUSE-Improving-Performance-of-User-File-Systems-Ashish-Bijlani-Georgia-Tech.pdf) - Considers using eBPF.

# eBPF in Security

* [TripleCross](https://github.com/h3xduck/TripleCross) ⭐ 1,978 | 🐛 19 | 🌐 C | 📅 2024-04-07 - A Linux eBPF rootkit with a backdoor, C2, library injection, execution hijacking, persistence and stealth capabilities.
* [ebpfkit](https://github.com/Gui774ume/ebpfkit) ⭐ 855 | 🐛 4 | 🌐 C | 📅 2023-02-28 - A rootkit that leverages multiple eBPF features to implement offensive security techniques.
* [Bad BPF](https://github.com/pathtofile/bad-bpf) ⭐ 697 | 🐛 2 | 🌐 C | 📅 2024-07-07 - A collection of malicious eBPF programs that make use of eBPF's ability to read and write user data in between the usermode program and the kernel.
* [ebpfkit-monitor](https://github.com/Gui774ume/ebpfkit-monitor) ⭐ 144 | 🐛 2 | 🌐 C | 📅 2023-02-28 - An utility to statically analyze eBPF bytecode or monitor suspicious eBPF activity at runtime. It was specifically designed to detect ebpfkit.
* [Embrace The Red: Offensive BPF!](https://embracethered.com/blog/tags/ebpf) - A series of posts around the introduction into BPF with a focus to an offensive setting, and also how its misuse can be detected. Posts include discussions on the rootkit capabilities of eBPF, or on which tracing type is needed for different use cases.
* [eBPF: Block Linux Fileless Payload "Malware" Execution with BPF LSM](https://djalal.opendz.org/post/ebpf-block-linux-fileless-payload-execution-with-bpf-lsm/) - Blog post about how BPF can help detection and blocking fileless malware.
* [Blackhat 2021: With Friends Like eBPF, Who Needs Enemies?](https://www.blackhat.com/us-21/briefings/schedule/#with-friends-like-ebpf-who-needs-enemies-23619) - Talk about an eBPF rootkit and how the capabilities of eBPF could be abused. The rootkit was also the object of a talk at Defcon, [eBPF, I thought we were friends !](https://defcon.org/html/defcon-29/dc-29-speakers.html#fournier).

## The Code

* [linux/include/linux/bpf.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/linux/bpf.h) - with [linux/include/uapi/bpf.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/uapi/linux/bpf.h): definitions related to eBPF, to be used respectively in the kernel and to interface with userspace programs.

* [linux/include/linux/filter.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/linux/filter.h) - with [linux/include/uapi/filter.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/uapi/linux/filter.h): information used to run the BPF programs themselves.

* [linux/kernel/bpf/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf) - This directory contains most of BPF-related code. In particular, those files are worth of interest:

  * [`syscall.c`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf/syscall.c) - Different operations permitted by the system call, such as program loading or map management.
  * [`core.c`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf/core.c) - BPF interpreter.
  * [`verifier.c`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf/verifier.c) - BPF verifier.

* [linux/net/core/filter.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/core/filter.c) - Functions and eBPF helpers related to networking (TC, XDP etc.); also contains the code to migrate cBPF bytecode to eBPF (all cBPF programs are translated to eBPF in recent kernels).

* [linux/kernel/trace/bpf\_trace.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/trace/bpf_trace.c) - Functions and eBPF helpers related to tracing and monitoring (kprobes, tracepoints, etc.).

* The JIT compilers are under the directory of their respective architectures, such as file [linux/arch/x86/net/bpf\_jit\_comp.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/net/bpf_jit_comp.c) for x86. Exception is made for JIT compilers used for hardware offload, sitting in their drivers, such as [linux/drivers/net/ethernet/netronome/nfp/bpf/jit.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/net/ethernet/netronome/nfp/bpf/jit.c) for Netronome NFP.

* [linux/net/sched/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/sched) - and in particular in files `act_bpf.c` (action) and `cls_bpf.c` (filter): code related to BPF actions and filters with TC.

* [linux/kernel/seccomp.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/seccomp.c)

* [linux/net/core/dev.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/core/dev.c) - contains the function `dev_change_xdp_fd()` that is called through a Netlink command to hook a XDP program to a device, after is has been loaded into the kernel from user space. This function in turns uses a callback from the relevant driver.

## Development and Community

* [The XDP Collaboration Project](https://github.com/xdp-project/xdp-project) ⭐ 314 | 🐛 6 | 🌐 CSS | 📅 2026-08-12 - A GitHub repository with notes and ideas regarding the future evolutions of XDP.
* [The bpf-next tree](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/) - BPF patches land in this tree. It is regularly merged into [net-next](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git), which is itself merged for each release to Linus' tree.
* [Kernel documentation](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git/tree/Documentation/bpf/bpf_devel_QA.rst) - About contributions to BPF.
* [The netdev mailing list](http://lists.openwall.net/netdev/) - Mailing list for Linux kernel networking stack development. All patches are sent there for review and inclusion.
* [XDP-newbies](http://vger.kernel.org/vger-lists.html#xdp-newbies) - A mailing list specially dedicated to XDP programming (both for architecture or for asking for help).

## Other Lists of Resources on eBPF

* [IO Visor's bcc documentation](https://github.com/iovisor/bcc/tree/master/docs) ⭐ 22,650 | 🐛 1,073 | 🌐 C | 📅 2026-08-27
* [IO Visor's bpf-docs repository](https://github.com/iovisor/bpf-docs/) ⭐ 1,017 | 🐛 3 | 📅 2022-09-20
* [Dive into BPF: A List of Reading Material](https://qmonnet.github.io/whirl-offload/2016/09/01/dive-into-bpf/)

## Acknowledgement

Thank you to Quentin Monnet and Daniel Borkmann for their original work on [Dive into BPF: A List of Reading Material](https://qmonnet.github.io/whirl-offload/2016/09/01/dive-into-bpf/) which became the basis for this list. Thanks to [@zoidyzoidzoid](https://github.com/zoidyzoidzoid/) for creating this document.

## Contributing

Contributions welcome! Read the [contribution guidelines](contributing.md) first.

## License

[![CC0](http://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](http://creativecommons.org/publicdomain/zero/1.0)

To the extent possible under law, the authors have waived all copyright and related or neighboring rights to this work.

***

> _Enhansomed by [enhansome](https://github.com/enhansome) on 2026-09-01._
