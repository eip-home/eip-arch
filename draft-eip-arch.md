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

 Introduction

## Networking architecture evolution

### Solutions above the layer 3

### Clean slate revolution

### Evolutionary solutions 

and the SRv6 Programming Model

# Basic principles for EIP


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
