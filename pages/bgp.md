---
layout: two-cols-header
transition: none
---
# "BGP: Bloody Good Protocol" - Mark Turner

::left::

- I like dynamic routing and I cannot lie
- You other methods can't deny

BGP with some tighter BFD timers is our solution of choice here. eBGP sessions, with private ASNs works well for our use case.

Any public IP allocations that get advertised back into our internet VRF will have these ASNs stripped on export to other networks.

::right::

<img src="/bgp.jpg">

<!--
The firewalls need some way to learn the routes from the internet and internal connectivity VRFs though. Just build some static routes and call it a day, right?

No. Please no. Dynamic where you can, static where you must.

We're using BGP to provide the routing information, with a session per role, being internet and internal, and per PE. This gives us 4 sessions to play with on the FortiGates. We have one PE in a primary role, and one in a secondary, so we use traffic engineering to prefer one of the links at all times, and only fail over when necessary. There's more than ample bandwidth available for this network, so we aren't needing to use both links at the same time. I'd love to use both at the same time, however we're at the mercy of the firewall platform here.

As the connectivity between the FortiGates and the Juniper MXes is only logically adjacent and not physically adjacent, we decided that BFD was the best way for us to handle signalling down the logical link. This is running on 100ms timers with an interval of 3, as we aren't seeing any significant hit to CPU load at this level. As we are leaving BFD to handle the heavy lifting of tearing down sessions, we have left all other BGP configuration, such as timers, to use the platform defaults.
-->
