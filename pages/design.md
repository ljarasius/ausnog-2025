# Upgrades people, upgrades

<img src="/design.svg" width=700px class="ml-20">

<!--
What about connecting it all together though? Well, Layer 3 connectivity comes from our existing Provider Edge infrastructure on Juniper MX series routers. The other side of the point-to-point connectivity goes over a pseudowire to our Label Edge Routers, which uses Ciena's 5000 series routing platform.
We are using Martini-style LDP pseudowires, so there is a targeted LDP session between the PE and LER to facilitate these connections.

We have been deploying the majority of our transit and L3VPN services this way for over a year now, with all LER provisioning handled by Ciena's Navigator Network Control Suite platform, and have been very impressed with the solution.

Across all of this, we can then connect devices from outside of the fabric to devices behind the fabric in a way that provides a high level of redundancy. We can then use this to deliver DC to DC connectivity, as well as internet circuits to our firewalls, which are clusters of Fortinet FortiGates.
-->
