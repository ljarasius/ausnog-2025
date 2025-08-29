# Our solution

We decided that it would be best to go back to the drawing board, rather than try and keep the existing network. This allows us to tackle all of the key issues, whilst also taking advantage of newer protocols and faster interface speeds.

- EVPN-VXLAN
- Standardising the design
- Hardware refresh
- ESI
- Orchestration tooling
- Telemetry streaming

https://www.juniper.net/documentation/us/en/software/apstra6.0/apstra-user-guide/topics/topic-map/evpn-support-addendum.html

https://www.juniper.net/documentation/us/en/software/apstra6.0/apstra-user-guide/topics/topic-map/devices-qualified.html

<!--
So, how are we going to solve this? Well, put simply, out with the old and in with the new. We decided that the best way to modernise our software stack, was to modernise the hardware stack first.

I'm sure that most people here have had some battles with spanning tree over the years. We knew there was a better way that had emerged since the old network was built, and that is VXLAN. Why switch when you can route? As a team of engineers that love label switching, this was a pretty easy argument to win. Couple that with EVPN for signalling, you've got a great stack that is well supported by many vendors.

To solve the issue of differing designs, we decided to pick something rather simple and straightforward, which we could expand on as required. This ended up being a spine and leaf deployment, rather than just being collapsed with a pair of switches, to allow us to add more switches as required.

We decided to stay with Juniper as our vendor of choice for the network, as Junos is what the team is familiar with across not just the existing data centre network, but also our MPLS network. The QFX5120 series was chosen as the leafs, and the QFX5200 series for the spine. 

The 5200 boxes are cheaper for flat 100G connectivity as opposed to the comparable 5120 variant, however the Broadcom Tomahawk ASIC on the inside doesn't work well in the leaf role. For frames that are already encapsulated with VXLAN and do not require de-encapsulation however, it is rather well suited. Limitations like this is something that is a little hard to wrap your head around at first, and the vendors often don't do a great job of making it clear.

Thankfully our SE helped us down the right path, however not everyone has access to someone at their vendor of choice, especially if you're deploying used hardware. I've had a few discussions with others over the years about what box works in what role as they have had the exact same questions, and I generally point to the two links on screen from Juniper. There's a good list of what boxes works in what role, and even if your device isn't covered, it lists the majority of chipsets that you would use for something like this and you can work backwards from there.

For automating the network, we settled on Juniper's Apstra platform. It is quite feature rich, and we found it to be quite intuitive for assisting in the standup of the fabrics. There's some great functionality in there too for automating the allocation of prefixes and ASNs for the eBGP underlay, as well as VNIs for the individual networks.

As part of Apstra, we also get telemetry streaming for visibility out of the box. This is something that we were wanting to dip our toes into with other parts of the network, so starting with the data centre fabric made a lot of sense. Apstra gives us pretty much everything we want out of the box, and being an intent based solution, it can correlate most of the issues for us and provide a root cause without needing someone to dig through the logs and make sense of what is going on.
-->
