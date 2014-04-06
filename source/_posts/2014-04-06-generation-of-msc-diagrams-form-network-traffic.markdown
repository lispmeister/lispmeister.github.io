---
layout: post
title: "Generation of MSC Diagrams form Network Traffic"
date: 2014-04-06 17:14
comments: true
categories: [research, network, tcp, programming, design]
---

{% img right /images/2014/04/generation-of-MSC-diagrams-from-network-traffic.png 250 250 'Generation of MSC Diagrams from Network Traffic' 'Generation of MSC Diagrams from Network Traffic' %}

I'm trying to work out a way to auto-generate message flow diagrams
from method calls or traces in log files. Here I found a paper that
shows how to do that for TCP/IP network traffic logs.

{% blockquote Viktor Borza | http://deeprecursion.com/file/2014/04/Generation-of-MSC-Diagrams-from-Network-Traffic.pdf Generation of MSC Diagrams from Network Traffic %}
Message Sequence Chart (MSC) diagrams were designed for modeling of
message-based communication between entities in the network. They are
used primarily by developing of a new network protocol as a
description of design requirements. However, MSC can be as well used
for visualization of real traffic captured from a network. One of the
applications aimed at work with MSC formalism is Sequence Chart Studio
(SCStudio), which is being developed in research centre Institute for
Theoretical Computer Science at FI MUNI.

The thesis is focused on the problem of generating Message Sequence
Chart (MSC) diagrams from PCAP (packet capture) file format. This
functionality was integrated into SCStu- dio as a new feature for
importing PCAP files. This paper describes the developing process and
behaviour of implemented functionality.
{% endblockquote %}

Of course there is also [TraceUML](http://trace2uml.tigris.org/) to
generate sequence diagrams from log statements. Alas, I really want
something that generates [Mscgen](http://www.mcternan.me.uk/mscgen/)
source.

