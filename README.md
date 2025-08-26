# BFD going down... from BGP timers expiring?

This repository houses my AusNOG 2025 talk, entitled _BFD going down... from BGP timers expiring?_. The following excerpt is from my proposal submission for consideration by the AusNOG 2025 Program Committee.

> The topic of this talk is exploring the BFD implementation in Junos, and the unexpected behaviour now documented in Juniper Networks knowledge base article KB97136 after our discovery at 5G Networks.
>
> BFD is often taken for granted, because it is generally such a robust protocol, therefore exploring the thought process of why testing it is actually working would be beneficial to many network operators running Junos as well as other network platforms.
>
>This talk would also touch on our network architecture choices for delivering L3VPNs and transit over Pseudowire Headend Termination (PWHT) using a VPLS circuit over a SR-MPLS core, and then interconnecting this into our new DC fabric running EVPN-VXLAN. A design like this provides a great example of places where BFD makes sense to use, due to many places where breaking the flow of frames between either end of the circuit would not result in physical interfaces being signalled down.

## Licence

&copy; Louis Jarasius 2025. MIT. See LICENCE.md for more information.