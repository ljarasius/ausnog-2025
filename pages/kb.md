---
layout: quote
transition: none
---

# "How issue is fixed in newer release is unidentified"

KB97136 - Juniper Networks Knowledge Base

https://supportportal.juniper.net/s/article/Singlehop-BFD-session-for-BGP-client-from-IRB-interface-of-VPLS-with-no-CE-facing-physical-interface-remain-up-after-connectvity-lost

<!--
And now we have this knowledge base article, immortalised on the internet! Want to fix this issue if you hit it? Restart the PPM daemon, or reboot the box. Fixed. Gone. Won't come back on the software installation you're running.

This bug only affects the first boot on an affected version, which had never even occurred to us that something like this was possible before going down this rabbit hole. Surely, after upgrading a device and it boots into the OS, it should be the same as every subsequent boot? Apparently that isn't always the case.

The article mentions that only 21.2R3-S2 is known to be affected. Is that the only version impacted? We don't think so, and the final line sums why we believe so.

"How this issue is fixed in newer release is unidentified."
-->
