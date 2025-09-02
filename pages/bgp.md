---
layout: two-cols-header
transition: none
---
# "BGP: Bloody Good Protocol" - Mark Turner

::left::

- I like dynamic routing and I cannot lie
- You other methods can't deny

BGP with some tighter BFD timers is our solution of choice here. eBGP sessions, with private ASNs works well for our use case.

Any public IP allocations that get advertised back into our internet VRF will not have the private ASNs advertised anywhere else, as we nail down our aggregates using BGP communities and only export on a match in the policy.

::right::

<img src="/bgp.jpg">

<!--
The firewalls need some way to learn the routes from the internet and internal connectivity VRFs though. Just build some static routes and call it a day, right?

No. Please no. Dynamic where you can, static where you must.

We're using BGP to provide the routing information, with a session per role, being internet and internal, and per PE. This gives us 4 sessions to play with on the FortiGates, per IPv4 and IPv6 address family, for a total of 8. We have one PE in a primary role, and one in a secondary role, so we use traffic engineering here to prefer one of the links at all times, and only fail over when necessary. There's more than ample bandwidth available on a single link for this network, so we aren't needing to use both links at the same time. I'd love to use both at the same time, however we're at the mercy of the firewall platform here.

As the connectivity between the FortiGates and the Juniper MXes is only logically adjacent, and not physically adjacent, we decided that BFD was the best way for us to handle signalling down the logical link. This is running on 100ms intervals with a multiplier of 3, as in our testing we weren't seeing any noticeable hit to CPU load. As we are leaving BFD to handle the heavy lifting of tearing down sessions, we have left all other BGP configuration, such as timers, to use the platform defaults.

The firewalls have their small aggregates on public IP address space they advertise back using a private ASN per cluster and VDOM, and the respective sub /24 and /48 IPv4 and IPv6 allocations only live within our ASN.

We heavily utilise BGP communities to control our internet VRF export policies, with our policies looking for specific matches before allowing a prefix to be sent to another network. This helps to ensure that we aren't externally advertising these smaller routes out, however in other parts of the network this also ensures that we don't create route leaks for prefixes with an AS path that we aren't authoritative for.
-->
