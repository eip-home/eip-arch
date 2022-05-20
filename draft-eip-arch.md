---
title: "Extensible In-band Processing (EIP) Architecture and Framework"
abbrev: "EIP Architecture"
category: info

docname: draft-eip-arch-latest
#submissiontype: independent  # also: "independent", "IAB", or "IRTF", "IETF"
ipr: trust200902
#number:
#date:
#consensus: true
#v: 3
area: AREA
workgroup: WG Working Group
keyword:
 - IPv6
 - Extension Headers
venue:
  group: EIP
  type: SIG
  mail: eip@cnit.it
  arch: http://postino.cnit.it/cgi-bin/mailman/private/eip/
  github: eip-home/eip-arch
  latest: https://eip-home.github.io/eip-headers/draft-eip-arch.html

stand_alone: yes
smart_quotes: no
pi: [toc, sortrefs, symrefs]

### for help with the syntax, see https://github.com/cabo/kramdown-rfc

author:
 -
    name: "Stefano Salsano"
    organization: Univ. of Rome Tor Vergata / CNIT
    email: "stefano.salsano@uniroma2.it"
 -
    name: "Hesham ElBakoury"
    organization: Consultant
    email: "helbakoury@gmail.com"

normative:

informative:
  id-eip-use-cases:
    title: "Extensible In-band Processing (EIP) Use Cases"
    author: 
     -
        name: "Stefano Salsano"
        ins: "S. Salsano"
        organization: Univ. of Rome Tor Vergata / CNIT
        email: "stefano.salsano@uniroma2.it"
     -
        name: "Hesham ElBakoury"
        ins: "H. ElBakoury"
        organization: Consultant
        email: "helbakoury@gmail.com"
    date: 2022
    seriesInfo: 
       Internet-Draft: draft-eip-use-cases
    format:
       TXT: "https://eip-home.github.io/eip-headers/draft-eip-use-cases.txt"
  id-eip-headers:
    title: "Extensible In-band Processing (EIP) Headers Definitions"
    author: 
     -
        name: "Stefano Salsano"
        ins: "S. Salsano"
        organization: Univ. of Rome Tor Vergata / CNIT
        email: "stefano.salsano@uniroma2.it"
     -
        name: "Hesham ElBakoury"
        ins: "H. ElBakoury"
        organization: Consultant
        email: "helbakoury@gmail.com"
    date: 2022
    seriesInfo: 
       Internet-Draft: draft-eip-headers-definitions
    format:
       TXT: "https://eip-home.github.io/eip-headers/draft-eip-headers-definitions.txt"


--- abstract

Extensible In-band Processing (EIP) extends the functionality of the IPv6 protocol considering
the needs of future Internet services / 6G networks. This document discusses the architecture and
framework of EIP. Two separate documents respectively analyze a number of use cases for EIP and provide
the protocol specifications of EIP.

--- middle

# Introduction

Networking architectures need to evolve to support the needs of future Internet services and 6G networks.
The networking research and standardization communities are considering different approaches for this evolution, we can broadly classify them in 3 different categories:

1. Clean slate and "revolutionary" solutions. Throw away the legacy networking layer (IP).
2. Solutions above the layer 3. Do not touch the legacy networking layer (IP). 
3. Evolutionary solution. Improve the IP layer (and try to preserve backward compatibility).

The proposed EIP (Extensible In-band Processing) solution belongs to the third category, it extends the current IPv6 architecture without requiring a clean-slate revolution. 

The use cases for EIP are discussed in [id-eip-use-cases]. The specification of the EIP header format
is provided in [id-eip-headers].

In the next subsection we will briefly mentions some solutions belonging to the three categories and in particular we will show how the "evolutionary" trend has already started and is progressing at a strong pace, for example with the SRv6 "Network Programming Model" and with the "In-band Telemetry".  

## Networking architecture evolution

### Solutions above the layer 3

### Clean slate revolution

### Evolutionary solutions 

and the SRv6 Programming Model

# Basic principles for EIP

The design the IP networking layer has been strongly influenced by the so called "end-to-end" concept, which prescribed putting "complex" functions in the IP hosts and "simple" functions in network forwarding devices (IP routers). Network operators have been used additional layers (e.g. ATM and then MPLS) to put the "complex" functions that are needed to run operators networks (backbones and access networks). We can also mention that in the real world, the end-to-end concept has been often disregarded with the introduction of middleboxes devices like NATs, TCP accelerators, but this has been seen as an unavoidable "mistake" and a problem. 

Recently we observe a clear trend in extending the functionality of the IP networking layer, going beyond the plain packet forwarding. An example of this trend is the rise of the SRv6 "network programming" model. With the SRv6 network programming models, the routers can implement "complex" functionalities and they can be controlled by a "network program" that is embedded in IPv6 packet headers. The operators can find all the needed functionality in the IPv6/SRv6 dataplane with no need of middleboxes nor of a separate MPLS layer. Another example is the INT (IN band Telemetry) solution for monitoring. 

We believe that this trend is fundamental for the future proof evolution of networking architectures and it should be pursued further. We envisage a feature-rich, extensible and programmable IPv6 networking layer, in which the intelligence is distributed across end-hosts, routers, virtual functions, servers in datacenters so that services can be implemented in the smartest and more efficient way. 

* Both end nodes and routers can read/write EIP information

* Limited domain applicability

* Tunneling concept

* Edge to edge, edge to server-end

* EIP header


# Benefits of a common EIP header for multiple use cases.

The EIP header will carry different EIP Information Elements that are defined to support the different use cases.
There are reasons why it is beneficial to define a common EIP header that support multiple use cases.

1. The number of available Option Types in HBH header is limited, likewise the number of available TLVs in the Segment Routing Header (SRH) is limited. Defining multiple Option Types or SRH TLVs for multiple use case is not scalable and puts pressure on the allocation of such codepoints.

2. The definition and standardization of specific EIP Information Elements for the different use cases is much simpler, rather than requiring the definition of a new Option Type or SRH TLVs.

3. Different use cases may share the EIP Information Elements.

4. Efficient and "Hardware Friendly" mechanisms can be defined when the different EIP Information Elements are carried inside the same EIP header.



# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
