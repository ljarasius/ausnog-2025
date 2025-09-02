# BFD going down... from BGP timers expiring?

<b>Louis Jarasius</b><br>
Senior Network Engineer<br>
5G Networks<br>
AusNOG 2025

<!--
An Extreme Networks switch walks into a bar. The bartender asks "What can I do for you today?". The Extreme switch replies, "I'll have a BGP session". The bartender says "Sure! Do you want it with this new BGP route attribute?". Naturally, not understanding what the new attribute was, nor how to implement RFC 7606, the Extreme switch falls off the chair and onto the ground.

BGP is a great protocol. BFD is also a great protocol. Together, they make quite a good team. Quick show of hands, who here has configured BFD before on a BGP session? 

Awesome, and who here can say that they've tested it works properly under a failure condition?

Today we explore what happens when that doesn't go as expected, and what we found over at 5G Networks.
-->
