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

Seeing that we're gluing pseudowires and VXLAN tunnels together, this is a good candidate for where something can go wrong along the way and break connectivity, likely from human error. So, let's simulate the human error!

As all the switching configuration is handled by Apstra, we can just remove the VLAN from the blueprint to simulate this scenario. This won't signal anything to the devices at either end, being our routers and firewalls, it will just drop all frames - which is exactly what we want.

So, we decided to start with the primary service. We have enabled some other features on the FortiGates to evaluate multiple possible interfaces when building a session, so that if we fail over the external connectivity to the backup path, little to no packets should be lost as the session isn't needing to be rebuilt.

Time to test. We open up Apstra, remove the VLAN and hit apply. We wait a few seconds, and not a moment after we see the configuration being marked as applied to the switches, I lose my in-band web UI session to the FortiGate. We had been running ICMP to the firewall and a host behind it, both are no longer responding. He's dead, Jim.
-->

---
layout: center
transition: none
---

<img src="/testing2.jpg" width="400px">

<!--
Well that was unexpected. Okay, time to get onto the console port of the firewall and see what went wrong, because _surely_ it's not my Trio boxes.

Open up Lighthouse, find the OpenGear the active firewall member is plugged into, connect to the port... and before we can even go any further, ICMP messages start being replied to, and my HTTPS connection restores. Clearly that broke something, but then it fixed itself? Weird. Let's go digging further.

We decide the best way to do that, is to roll our changes back and see what happens. The firewall doesn't skip a beat. Not a single packet lost on our testing. Interesting. Double check interface graphs, and we've definitely switched back to the primary circuit.

Okay, let's give it another crack. But this time, we're on the console port on the firewall and poking around at what is going on. We drop the primary circuit, and once again the firewall stops responding to external connectivity. We check the BGP session for the circuit we're playing with, and it is down, just like we would expect. BFD seems to be working here as expected. Interesting. Everything else looks fine, nothing is jumping out at us as unexpected.

So we decide to change tact, and look at the MX terminating this circuit...
-->
