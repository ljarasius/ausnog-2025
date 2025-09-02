---
layout: two-cols
transition: none
---
# Implementation

- Rack and stack
- OOB connectivity
- Stand up migration VRF
- Build new links
- Initial configuration
- Software upgrades
- Validation

::right::

<img src="/implementation.svg">

<!--
We've got our design all sorted, so now it is time to implement it.

The data centres we are deploying this equipment in happen to be facilities that we own, so arranging for racks and power is all internal. Once those are ready, we have staff onsite to unbox all the equipment and install it for us.

One thing we made sure to do from day one was provide out-of-band console access to the equipment, so that we are always able to access the terminal no matter what happens. We have quite a few OpenGear devices using third-party circuits deployed across our network, so we can extend some connections from these back to the devices in the new racks. In the diagram on the right, you can also see there is a management firewall at the bottom, which is another separated network we have spun up with internet access, to ensure that we have another path in alongside our out-of-band console access, as well as for connectivity to our management and monitoring tools.

As part of providing that management and monitoring access, we have built a temporary L3VPN to connect the firewalls at the data centres together, as well as to leak some routes in from our existing management VRF so we can connect back to our existing systems and tooling.

So, now we have remote console and data access to the devices. This makes updating them and applying some basic configuration pretty straightforward. It's at this point, we also take the time here to update our internal documentation and build some diagrams, add the prefixes and IP addresses into IPAM, and add the devices into our monitoring system.
-->
