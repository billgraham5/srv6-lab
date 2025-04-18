# SRv6 TOI

This topology is built on Containerlabs and is intended to be an introduction to SRv6.  The following documentation will guide you on the implemenation:

- Implementing Containerlabs for XRd and SONiC (todo)
- Containerlabs CLI Cheat Sheet 
- IPv6 addressing planning for SRv6
- Interface configuration for SRv6
- Day 1 IS-IS configuration for SRv6
- Configuraton for Global IP Overlay Sevices (BGP-Free Core)
- SRv6 Automated Traffic Steering (BGP Locator-based Forwarding)
- Administrative Groups (Link Affinity) for SRv6 TE Policy
- Anycast-based BGP Routing (Egress Engineering for transit services)

In addition, the Containerlabs configuration file has been shared.  You will need to have a valid Cisco service contract to download XRd.  You can alternatively use SONiC or FRR, although functionality will vary.  SRv6 is an architecture that leverages a collection of hundreds of individual features.  Many are standardized but not all feature are implemented on all vendor implementations.

A topology diagram is provided for each major use case.  

# Use Case 1

Use case 1 leverages different flexible algorithms to implement a form of network slicing.  This scenario does not contain any SR Traffic Engineering policy, as it is not necessary to meet the objective.

The objective is steer certain traffic over the left side or right side of the topology.  Traffic steering is accmomplished via a route policy that matches specific prefixes and assigns those prefixes to a specific SRv6 Locator.  This policy is implemented as part of a standard IBGP export policy using a single SRv6 specific "set" command.

This topology is built upon the Global IP Overlay Services scenario.  This expands on the architecture developed for MPLS that is referred to as a "BGP Free Core".  It is similar to the routing paradigm where core routers in L3VPN deployments rarely ever carry inet-vpn (VPNv4) prefixes.  In this case, the address family is simply the global or main routing table for the IPv4 unicast AFI.  If the main routing table only carries the public internet routing table, this means the core routers will not need to carry any of these prefixes.  The MPLS implementation tunnels traffic via MPLS whereas the SRv6 implementation tunnels traffic simply inside of IPv6 tunnels.

# Use Case 2

Use case 2 does not require more than the default flexible algorithm.  In this case, SRv6 Traffic Engineering policy is defined to match traffic at ingress and apply an end-to-end TE policy.

Static policies configured on ingress to every egress node can be configured.  Alternatively, On-Demand Next-hop (ODN) can be leveraged as a configuratuon template that does not specificy specific egress nodes as an end-point.

In this scenario, Administrative Groups (Link Affinity) is used.  Link affniity was originally a MPLS concept that relies on "coloring" the links in your network and defining a policy that requires or prevents certain link colors from being used for the matching traffic.

