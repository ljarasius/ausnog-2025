---
layout: center
transition: none
---

<img src="/tac.jpg">

<!--
So now it is time to engage TAC. I think some of these memes will capture my slow descent into madness.
-->

---

# Vendor TAC fun

```
rpd[30554]: BGP_IO_ERROR_CLOSE_SESSION: BGP peer 192.0.2.1 (External AS 65032):
Error event Operation timed out(60) for I/O session - closing it (instance {{ vrf })

bfdd[29629]: BFDD_STATE_UP_TO_DOWN: BFD Session 192.0.2.1 (IFL 393) state Up -> Down
LD/RD(46/19) Up time:00:03:12 Local diag: AdminDown Remote diag: None Reason: Received Upstream Destroy Session.

bfdd[29629]: BFDD_TRAP_SHOP_STATE_DOWN: local discriminator: 46, new state: down,
interface: irb.1, peer addr: 192.0.2.1
```

That order doesn't seem right to me. Surely a bug, yes?

<!--
This is the log message that starts it all. We see the BGP session go down due to timeouts exceeding, which is completely fine if we didn't have BFD turned on, however we do. But then we see BFD go down, _after_ it? And what's the message?

"Received Upstream Destroy Session."

So BFD is staying up, despite getting no messages, BGP tears down due to timeouts, and then BFD follows suit as the session it was attached to is now gone. That's clearly a bug. Surely we won't have to explain that. Right? Right? Right?
-->

---
layout: center
transition: none
---

<img src="/tac2.jpg">

<!--
That would be too easy, wouldn't it. So, I hop on a call with the engineer working on our case,
-->

---

# Vendor TAC fun
