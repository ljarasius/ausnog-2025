---
layout: two-cols
transition: none
---
# Testing

- Remove VLAN from Apstra
- Simulate a configuration mishap
- Transparent to the devices at either end

What could go wrong?

::right::

<img src="/testing.jpg">

<!--
So we're all good to go. One of things we decided to test first was the external connectivity out of the fabric.

Seeing that we're gluing pseudowires and VXLAN tunnels together, this is a good candidate on where something can go wrong along the way and break connectivity, likely from human error. So, let's simulate the human error!

As all the switching configuration is handled by Apstra, we can just remove the VLAN from the blueprint, to simulate this scenario. This won't signal anything to the devices at either end, being our routers and firewalls, it will just drop all frames.

So, we do that, and everything looks good on the FortiGate. The BFD session has stopped seeing messages, and in turn torn itself and the attached BGP session down. However, on the MX...
-->
