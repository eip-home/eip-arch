---
title: "Extensible In-band Processing (EIP) Architecture and Framework"
abbrev: "EIP Architecture"
category: info

docname: draft-eip-arch-latest
submissiontype: independent # also: "independent", "IAB", or "IRTF", "IETF"
ipr: trust200902
#number: 0
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
    organization: "Univ. of Rome Tor Vergata / CNIT"
    email: "stefano.salsano@uniroma2.it"
 -
    name: "Hesham ElBakoury"
    organization: Consultant
    email: "helbakoury@gmail.com"
 -
    name: "Diego R. Lopez"
    ins: "D. Lopez"
    organization: "Telefonica, I+D"
    email: "diego.r.lopez@telefonica.com"

normative:

informative:
  RFC8754:
  RFC8986:
  RFC8799:
  RFC8250:
  RFC8321:
  RFC8558:
  I-D.ietf-ippm-ioam-data:
  I-D.ietf-ippm-ioam-ipv6-options:
  I-D.draft-ietf-6man-ipv6-alt-mark:
  I-D.draft-filsfils-spring-path-tracing:
  I-D.draft-ietf-6man-mtu-option:
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
       TXT: "https://eip-home.github.io/use-cases/draft-eip-use-cases.txt"
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
  onf-int:
    title: "Improving Network Monitoring and Management with Programmable Data Planes"
    author:
     -
        name: "P4.org"
    format:
       PDF: "https://opennetworking.org/news-and-events/blog/improving-network-monitoring-and-management-with-programmable-data-planes/"
    date: 2015
  int-spec:
    author:
     -
        name: "The P4.org Applications Working Group"
    title: "In-band Network Telemetry (INT) Dataplane Specification, version 2.1"
    format:
      PDF: "https://p4.org/p4-spec/docs/INT\_v2\_1.pdf"
      date: 2022

--- abstract

Extensible In-band Processing (EIP) extends the functionality of the IPv6 protocol considering
the needs of future Internet services / 6G networks. This document discusses the architecture and
framework of EIP. Two separate documents respectively analyze a number of use cases for EIP and provide
the protocol specifications of EIP.

--- middle

# Introduction

Networking architectures need to evolve to support the needs of future Internet services and 6G networks.
The networking research and standardization communities have considered different approaches for this evolution, that can be broadly classified in 3 different categories:

1. Clean slate and "revolutionary" solutions. Throw away the legacy IP networking layer.
2. Solutions above the layer 3. Do not touch the legacy networking layer (IP).
3. Evolutionary solutions. Improve the IP layer (and try to preserve backward compatibility).

The proposed EIP (Extensible In-band Processing) solution belongs to the third category, it extends the current IPv6 architecture without requiring a clean-slate revolution.

The use cases for EIP are discussed in [id-eip-use-cases]. The specification of the EIP header format is provided in [id-eip-headers].

# Basic principles for EIP

An ongoing trend is extending the functionality of the IPv6 networking layer, going beyond the plain packet forwarding. An example of this trend is the rise
of the SRv6 "network programming" model. With the SRv6 network programming model,
the routers can implement "complex" functionalities and they can be controlled
by a "network program" that is embedded in IPv6 packet headers. Another example is the INT (IN band Telemetry) solution for monitoring. These (and other) examples are further discussed in {{review}}.

The EIP solution is aligned with this trend, which will ensure a future proof evolution of networking architectures. EIP supports a feature-rich and extensible IPv6 networking layer, in which complex dataplane functions can be executed by end-hosts, routers, virtual functions, servers in datacenters so that services can be implemented in the smartest and more efficient  way.

The EIP solution foresees the introduction of an EIP header in the IPv6 packet header. The proposed EIP header is extensible and it is meant to support a number of different use cases. In general, both end-hosts and transit routers can read and write the content of this header. Depending of the specific use-case, only specific nodes will be capable and interested in reading or writing the EIP header. The use of the EIP header can be confined to a single domain or to a set of cooperating domains, so there is no need of a global, Internet-wide support of the new header for its introduction. Moreover, there can be usage scenarios in which legacy nodes can simply ignore the EIP header and provide transit to packets containing the EIP header.

An important usage scenario considers the transport of user packets over a provider network. In this scenario, we consider the network portion from the provider ingress edge node to the provider egress edge node. The ingress edge node can encapsulate the user packet coming from an access network into an outer packet. The outer packet travels in the provider network until the egress edge node, which will decapsulate the inner packet and deliver it to the destination access network or to another transit network, depending on the specific topology and service. Assuming that the IPv6/SRv6 dataplane is used in the provider network, the ingress edge node will be the source of an outer IPv6 packet in which it is possible to add the EIP header. The outer IPv6 packet (containing the EIP header) will be processed inside the “limited domain” (see {{RFC8799}}) of the provider network, so that the operator can make sure that all the transit routers either are EIP aware or at least they can forward packets containing the EIP header. In this usage scenario, the EIP framework operates “edge-to-edge” and the end-user packets are “tunneled” over the EIP domain.

The architectural framework for EIP is depicted in {{fig:eip-framework}}. We refer to nodes that are not EIP capable as legacy nodes. An EIP domain is made up by EIP aware routers (EIP R) and can also include legacy routers (LEG R). At the border of the EIP domain, EIP edge nodes (EIP ER) are used to interact with legacy End Hosts / Servers (LEG H) and with other domains. It is also possible that an End Host / Server is EIP aware (EIP H), in this case the EIP framework could operate “edge-to-end” or “end-to-end”.

~~~

                                                       LEG domain
                                                     +------------+

 +---+             +---+      +---+                +---+
 |EIP|_           _|EIP|______|EIP|             ___|LEG|
 | H | \__+---+__/ | R |      | R |__   +---+__/   | R | ...
 +---+    |EIP|    +---+      +---+  \__|EIP|      +---+
        __|ER |__    |          |     __|ER |__
 +---+_/  +---+  \_+---+      +---+__/  +---+  \___+---+
 |LEG|             |LEG|______|LEG|                |EIP|
 | H |             | R |      | R |                |ER | ...
 +---+             +---+      +---+                +---+

            +-----------------------------+          +------------+
                      EIP domain                       EIP domain

~~~
{: #fig:eip-framework title="EIP framwork"}

As shown in {{fig:eip-framework}}, an EIP domain can communicate with other domains, which can be legacy domains or EIP capable domains.


# Benefits of a common EIP header for multiple use cases.

The EIP header will carry different EIP Information Elements that are defined to support the different use cases.
There are reasons why it is beneficial to define a common EIP header that supports multiple use cases.

1. The number of available Option Types in HBH header is limited, likewise the number of available TLVs in the Segment Routing Header (SRH) is limited. Defining multiple Option Types or SRH TLVs for multiple use case is not scalable and puts pressure on the allocation of such codepoints. This aspect is further discussed in {{review}}.

2. The definition and standardization of specific EIP Information Elements for the different use cases will be simplified, compared to the need of requiring the definition of a new Option Type or SRH TLVs.

3. Different use cases may share a subset of common EIP Information Elements.

4. Efficient mechanism for the processing of the EIP header (both in software and in hardware) can be defined when the different EIP Information Elements are carried inside the same EIP header.

{: #review}
# Review of standardized and proposed evolutions of IPv6

In the last few years, we have witnessed important innovations in IPv6 networking, centered around the emergence of Segment Routing for IPv6 (SRv6) {{RFC8754}} and of the SRv6 "Network Programming model" {{RFC8986}}. With SRv6 it is possible to insert a *Network program*, i.e. a sequence of instructions (called *segments*), in a header of the IPv6 protocol, called Segment Routing Header (SRH).

Another recent activity that proposed to extend the networking layer to support more complex functions, concerns the network monitoring. The concept of INT “In-band Network Telemetry” has been proposed since 2015 {{onf-int}} in the context of the definition of use cases for P4 based data plane programmability. The latest version of INT specifications dates November 2020 {{int-spec}}. {{int-spec}} specifies the format of headers that carry monitoring instructions and monitoring information along with data plane packets. The specific location for INT Headers is intentionally not specified: an INT Header can be inserted as an option or payload of any encapsulation type. The In-band Telemetry concept has been adopted by the IPPM IETF Working Group, renaming it “In-situ Operations, Administration, and Maintenance” (IOAM). The internet draft {{I-D.ietf-ippm-ioam-data}} is about to become an IETF RFC. Note that IOAM is focused on “limited domains” as defined in {{RFC8799}}. The in-situ OAM data fields can be encapsulated in a variety of protocols, including IPv6. The specification details for carrying IOAM data inside IPv6 headers are provided in draft {{I-D.ietf-ippm-ioam-ipv6-options}}, which is also close to becoming an RFC. In particular, IOAM data fields can be encapsulated in IPv6 using either Hop-by-Hop Options header or Destination options header.

Another example of extensions to IPv6 for network monitoring is specified in {{RFC8250}}, which defines an IPv6 Destination Options header called Performance and Diagnostic Metrics (PDM). The PDM option header provides sequence numbers and timing information as a basis for measurements.

The “Alternate Marking Method” is a recently proposed performance measurement approach described in {{RFC8321}}. The draft {{I-D.draft-ietf-6man-ipv6-alt-mark}} (also close to becoming an RFC) defines a new Hop-by-Hop Option to support this approach.

“Path Tracing” {{I-D.draft-filsfils-spring-path-tracing}} proposes an efficient solution for recording the route taken by a packet (including timestamps and load information taken at each hop along the route). This solution needs a new Hop-by-Hop Option to be defined.

{{RFC8558}} analyses the evolution of transport protocols. It recommends that explicit signals should be used when the endpoints desire that network elements along the path become aware of events related to trasport protocol. Among the solutions, {{RFC8558}} considers the use of explicit signals at the network layer, and in particular it mentions that IPv6 hop-by-hop headers might suit this purpose.

The Internet Draft {{I-D.draft-ietf-6man-mtu-option}} specifies a new IPv6 Hop-by-Hop option that is used to record the minimum Path MTU between a source and a destination. This draft is close to become an RFC.

## Consideration on Hop-by-hop Options allocation

We have listed several proposals or already standardized solutions that use the IPv6 Hop-by-Hop Options. These Options are represented with a 8 bits code. The first two bits represent the action to be taken if the Options is unknown to a node that receives it, the third bit is used to specify if the content of the Options can be changed in flight. In particular the Option Types that start with 001 should be ignored if unknown and can be changed in flight, which is the most common combination. The current IANA allocation for Option Types starting with 001 is
   (see https://www.iana.org/assignments/ipv6-parameters/ipv6-parameters.xhtml)

~~~
   32 possible Option Types starting with 001
   2 allocated by RFCs
   2 temporary allocated by Internet Drafts
   1 allocated for RFC3692-style Experiment
   27 not allocated
~~~

We observe that there is a potential scarcity of the code points, as there are many scenarios that could require the definition of a new Hop-by-hop option. We also observe that having only 1 code point allocated for experiments is a very restrictive limitation.

# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations

TODO Security


# IANA Considerations

The definition of the EIP header as an Option for IPv6 Hop-by-hop Extension header requires the allocation of a codepoint from the "Destination Options and Hop-by-Hop Options" registry in the "Internet Protocol Version 6 (IPv6) Parameters" (https://www.iana.org/assignments/ipv6-parameters/ipv6-parameters.xhtm).

The definition of the EIP header as a TLV in the Segment Routing Header requires the allocation of a codepoint from the "Segment Routing Header TLVs" registry in the "Internet Protocol Version 6 (IPv6) Parameters" (https://www.iana.org/assignments/ipv6-parameters/ipv6-parameters.xhtm).

The definition of EIP Information Elements in the EIP header will require the definition of a IANA registry.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
