# Notes about VXLAN and hardware

Devices:
<br>
https://www.juniper.net/documentation/us/en/software/apstra6.0/apstra-user-guide/topics/topic-map/devices-qualified.html

Chipsets:
<br>
https://www.juniper.net/documentation/us/en/software/apstra6.0/apstra-user-guide/topics/topic-map/evpn-support-addendum.html

<!--
One thing that isn't clear to a lot of people doing their first deployment of a VXLAN fabric, is that not every device can perform well in every function. It's kind of like how lots of chipsets support MPLS, however things like maximum label depth can vary drastically.

In our use case, the 5200 boxes are cheaper for flat 100G connectivity as opposed to the comparable 5120 variant, however the Broadcom Tomahawk ASIC on the inside doesn't work well in the leaf role. For frames that are already encapsulated with VXLAN and do not require de-encapsulation however, it is rather well suited. Limitations like this is something that is a little hard to wrap your head around at first, and the vendors often don't do a great job of making it clear.

Thankfully our Juniper SE helped us down the right path, however not everyone has access to someone at their vendor of choice, especially if you're deploying used hardware. I've had a few discussions with other people over the years about what box works in what role, as they have had the exact same questions, and I generally point to the two links on screen from Juniper. There's a good list of what boxes works in what role, and even if your device isn't covered, the second link has the majority of chipsets that you would use for something like this, with the roles they perform best in, and you can work backwards from there.
-->
