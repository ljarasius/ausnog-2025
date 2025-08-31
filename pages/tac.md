---
layout: center
transition: none
---

<img src="/tac.jpg">

<!--
Here begins my slow descent into madness. Please keep your hands and feet inside the vehicle at all times, it's going to be a bumpy ride.
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
That would be too easy, wouldn't it. So, I hop on a call with the engineer working on our case, spend two hours explaining our architecture and use case, reproducing the issue again, and answering questions. This is all recorded by the engineer for them to come back to as needed. All the tracebacks, log dumps and terminal scrollbacks added to the case.

Surely we're done here for troubleshooting, and the issue is clear?
-->

---

# Vendor TAC fun

```
Received Downstream RcvPkt (19) len 110:
  IfIndex (3) len 4: 393
  Protocol (1) len 1: BFD
  SrcAddr (5) len 8: 192.0.2.1
  Data (9) len 24: (hex) {{ data }}
  PktError (26) len 4: 0
  RtblIdx (24) len 4: 16
  MultiHop (64) len 1: (hex) 00
  Seamless (245) len 1: 0
  Unknown (213) len 1: (hex) 00
  Unknown (261) len 4: (hex) 00 00 0e c8
  Unknown (168) len 1: (hex) 00
  Authenticated (121) len 1: (hex) 0
```

TAC: "Our MX side’s BFD is single hop, Fortigate bfd is multi hop."

Me: ...

<!--
TAC come back with this gem.

"Our MX side's BFD is single hop, Fortigate bfd is multi hop.", and have the MultiHop data as well as the Seamless and Unknown data below it highlighted.

Right, we're clearly on different pages. No multi hop here, and not to mention their notes are also saying that they couldn't get a configuration like that to work in their lab. No issue with bringing _up_ our BFD session, all the problems are with tearing it down.

For the eagle eyed amongst us here, yes the MultiHop bit is set to 0. And yes, the only other option that was highlighted, being 261, the hex data there equals 3784 in decimal, which is the single hop BFD port.
-->

---
layout: center
transition: none
---

<img src="/tac3.jpg" width="300px">

<!--
So, we push back. Multihop isn't here at all, the configuration on the FortiGate was also shown to the engineer on the recorded call.

And so what's next? You guessed it, we're told that once again, multihop is the cause here and we need to enable it on our MX to bring up the BFD session.

It's at this point we decided that we're getting no where, and pushed for an escalation to a higher level team.
-->

---

# Vendor TAC fun

```
PPM Trace: BFD periodic xmit to 192.0.2.1 (IFL 393, rtbl 16, single-hop port)
PPM Trace: BFD packet from 192.0.2.1 (IFL 393, rtbl 16, ttl 255) absorbed
PPM Trace: BFD periodic xmit to 192.0.2.1 (IFL 393, rtbl 16, single-hop port)
PPM Trace: BFD packet from 192.0.2.1 (IFL 393, rtbl 16, ttl 255) absorbed
PPM Trace: BFD periodic xmit to 192.0.2.1 (IFL 393, rtbl 16, single-hop port)
PPM Trace: BFD packet from 192.0.2.1 (IFL 393, rtbl 16, ttl 255) absorbed
PPM Trace: BFD periodic xmit to 192.0.2.1 (IFL 393, rtbl 16, single-hop port)
PPM Trace: BFD periodic xmit to 192.0.2.1 (IFL 393, rtbl 16, single-hop port)
PPM Trace: BFD periodic xmit to 192.0.2.1 (IFL 393, rtbl 16, single-hop port)
PPM Trace: BFD periodic xmit to 192.0.2.1 (IFL 393, rtbl 16, single-hop port)
PPM Trace: BFD periodic xmit to 192.0.2.1 (IFL 393, rtbl 16, single-hop port)
PPM Trace: BFD periodic xmit to 192.0.2.1 (IFL 393, rtbl 16, single-hop port)
```

PR1845344 raised. Making some progress.

<!--
Our escalation is successful. Yay!

After a few questions back and forth to understand the case, the engineer sends us this output that they found. We can see that the BFD daemon stops seeing messages, however doesn't log anything about dropping the session and keeps on transmitting messages. This is exactly the behaviour we have been seeing, as the session stays marked as Up on the MX, and these transmitting messages continue until our usual BGP down message followed by BFD being torn down due to nothing for it to be attached to.

The process of engaging engineering is started, and we are assigned a PR number. Success! We're moving forward.
-->
