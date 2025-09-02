# Our solution

We decided that it would be best to go back to the drawing board, rather than try and keep the existing network. This allows us to tackle all of the key issues, whilst also taking advantage of newer protocols and faster interface speeds.

- EVPN-VXLAN
- Standardising the design
- Hardware refresh
- ESI
- Orchestration tooling
- Telemetry streaming

<!--
So, how are we going to solve this? Well, put simply, out with the old and in with the new. We decided that the best way to modernise our software stack, was first to modernise the hardware stack.

I'm sure that most people here have had some battles with spanning tree over the years. We knew there was a better way that had emerged since the old network was built, and that is VXLAN. Why switch when you can route? As a team of engineers that love label switching, this was a pretty easy argument to win. Couple that with EVPN for signalling, you've got a great stack that is well supported by many vendors.

To solve the issue of differing designs, we decided to pick something rather simple and straightforward, which we could expand on as required. This ended up being a spine and leaf deployment, rather than just a pair of switches with redundant interlinks, to allow us to add more switches as required.

We decided to stay with Juniper as our vendor of choice for the network, as Junos is what the team is familiar with across not just the existing data centre network, but also our MPLS network. The QFX5120 series was chosen as the leafs, and the QFX5200 series for the spine. 

For automating the network, we settled on Juniper's Apstra platform. It is quite feature rich, and we found it to very useful for assisting in the standup of the fabrics. There's some great functionality in there too for automating the allocation of prefixes and ASNs for the eBGP underlay, as well as VNIs for the individual networks.

As part of Apstra, we also get telemetry streaming for visibility out of the box. This is something that we've wanting to dip our toes into with other parts of the network for a while, so starting with the data centre fabric made a lot of sense. Apstra gives us pretty much everything we want out of the box, and being an intent based solution, it can correlate most of the issues for us and provide a root cause, without needing someone to dig through the logs and make sense of what is going on.
-->
