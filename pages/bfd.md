# Hello? Hello? Hello?

```
louisj@pe1.pop1> show bfd session address 192.0.2.1 extensive    
                                                  Detect   Transmit
Address                  State     Interface      Time     Interval  Multiplier
192.0.2.1                Up        irb.1          0.300     0.100        3   
 Client BGP, TX interval 0.100, RX interval 0.100
 Session up time 00:03:59
 Local diagnostic None, remote diagnostic None
 Remote state Up, version 1
 Session type: Single hop BFD
 Min async interval 0.100, min slow interval 1.000
 Adaptive async TX interval 0.100, RX interval 0.100
 Local min TX interval 0.100, minimum RX interval 0.100, multiplier 3
 Remote min TX interval 0.100, min RX interval 0.100, multiplier 3
 Local discriminator 52, remote discriminator 37
 Echo TX interval 0.000, echo detection interval 0.000
 Echo mode disabled/inactive Session ID: 0x5f4
```

It's... still up?

<!--
We go looking at the BGP session, and it is still showing Established. Okay, so what's BFD doing then?

Wait, it hasn't torn down? There's clearly no messages coming in, the VLAN that trunks back to the psuedowire for this circuit doesn't exist on the switches.

We dig through the logs, and decide that this is definitely a bug and to take the next step. Time to engage the vendor.
-->

---

# Hello? Hello? Hello?

```
louisj@pe1.pop1> show bfd session address 192.0.2.1 extensive    

0 sessions, 0 clients
Cumulative transmit rate 0.0 pps, cumulative receive rate 0.0 pps
```

<!--
-->
