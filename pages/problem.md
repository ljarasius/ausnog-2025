---
layout: two-cols
transition: none
---
# What is the problem being solved?

5G Networks uses 3 primary sites to deliver internal and customer compute services, one in Sydney (SDC), one in Melbourne (MDC), and one in Adelaide (ADC). These networks are critical for business continuity, however are in need of a refresh after running successfully for many years.

- Ageing compute network infrastructure
- Spanning tree
- Lots of manual configuration for MACs
- MC-LAGs using virtual chassis
- Limited visibility
- Inconsistent design across facilities

::right::

<img src="/problem.jpg" width="400px" class="mt-20 ml-10">

<!--
One thing we've been wanting to tackle for a while is a refresh of our data centre networks. There is a lot internally that relies on them, and we want to ensure that as we upgrade the rest of our core network, this is not left behind with legacy solutions and hardware. We have 3 sites we use to deliver diversity, which has worked well for us, however there's a few challenges that we have been facing with the existing solution.

The existing network is running Juniper Networks QFX5100 series switches, which I'm sure is a pretty common choice over the years with many other operators in this room. They have been quite reliable, and did everything we needed when they were selected. However, they have been marked as End of Life from the vendor, and we need to start looking at longer term solutions to ensure that we have hardware and software support.

Secondly, being an older design means that there's some older technologies at play here. Spanning tree has its' place, however there is newer kids on the block that bring a lot of improvements. This network is using MSTP to try and help better use all available links, however I'm sure I am preaching to the converted that there are better options in a modern network.

Now, let's look at how we work on the devices day to day. Adding an existing VLAN to a port is pretty straightforward, but what about adding a new VLAN? Whole different ballgame. There's a lot of pairs of switches in the data centre networks, and having to go around multiple devices introduces room for error. This all makes general moves, adds and changes become tedious and time consuming.

How is high availability being handled for endpoints? Two member virtual chassis clusters are in use and this does work, and makes bringing up a new LAG pretty straightforward. However, who here has had to replace a member of a virtual chassis before? It's not fun, you can do everything right and the stack still falls apart. This poses a bigger risk as time goes on, as the hardware starts to exit the bottom of the bathtub curve and the chance of failure increases.

Even when things are running as expected, how can we assure that no redundant links have members down? How do we know that a VLAN isn't missing on a backup link? How can we know that we aren't just one wrong move away from having an outage to one or multiple parts of the fabric? Legacy SNMP monitoring solutions work well for individual data points, however this often takes a good understanding of the design to be able to piece something together, and isn't able to cover all the things we would like to see going forward.

Finally, these points stick across all 3 of the fabrics, however the underlying design is often quite inconsistent between them. This makes troubleshooting issues quite difficult for staff that aren't across all of the specific intricacies, and is something that we'd like to fix in the new solution.
-->
