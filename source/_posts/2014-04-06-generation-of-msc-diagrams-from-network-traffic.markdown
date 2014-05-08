---
layout: post
title: "Generation of MSC Diagrams from Network Traffic"
date: 2014-04-06 17:14
comments: true
categories: [research, network, tcp, programming, design, tracing]
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

Other sequence diagram generators:

- [TraceUML](http://trace2uml.tigris.org/) to generate sequence diagrams from log statements.
- [seqdiag](http://blockdiag.com/en/seqdiag/) is a Python tool.
- [mscpackage](http://satoss.uni.lu/software/mscpackage/) is a LaTeX package for drawing message sequence
diagrams that supports the full MSC2000 language.
- [Quick Sequence Diagram Editor](http://sdedit.sourceforge.net/) is a
  tool for creating UML sequence diagrams from textual descriptions of
  objects and messages.
- [JS Sequence Diagrams](http://bramp.github.io/js-sequence-diagrams/)
  is a simple javascript library to turn text into vector UML sequence diagrams. 
- [Jumly](http://jumly.tmtk.net/) is a JavaScript library for UML
  diagram rendering engine. It works completely on client side.
  
I'm currently using [Mscgen](http://www.mcternan.me.uk/mscgen/)
because I can edit and render diagram source in Emacs with org-mode.



