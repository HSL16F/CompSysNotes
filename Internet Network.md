The Internet/network [[Networks and layers|layer's]] purpose is to get data from the source to the destination.
![[Pasted image 20240526135235.png]]
It may not be a single hop (Point-to-point link).
Its critical that the traffic is routed efficiently, this is performed via [[Routers|routers]]
Nodes must be given an name/address for get to travel across the system.
![[Pasted image 20240526135253.png]]

The network layer code runs on routers and protocol data units are typically referred to as packets.
The network layer provides [[Connectionless]] and [[Connection-Oriented]] services.

#### Store and forward packet switching
Internet is a packet switched network
If say Host H1 wishes to send a packet to H2 the following steps proceed:
1. Transmit to nearest router (A)
2. Packet is buffered while it is arriving and the checksum is verified
3. If valid, packet is stored until outgoing interface is free
4. Router forwards packet onto next router of path
5. Steps 2-4 are repeated until destination achieved

**Connectionless example:**
![[Pasted image 20240526140526.png]]
Connection-Oriented example:
![[Pasted image 20240526140752.png]]

There are various pros and cons to both:

| Issue                | Datagram Network                                          | Virtual Circuit (VC)                                                   |
| -------------------- | --------------------------------------------------------- | ---------------------------------------------------------------------- |
| Type                 | [[Connectionless]]                                        | [[Connection-oriented]]                                                |
| State                | + Routers do not hold state information about connections | - Each VC requires router table space and router reboots are a problem |
| Addressing           | - Each packet has full source and destination             | + Each packet contains short VC number                                 |
| Routing              | Each packet independently                                 | Defined at set-up                                                      |
| Quality of Service   | - Difficult                                               | + Easy with enough resources                                           |
| Congestion control   | - Difficult                                               | + Easy with enough resources                                           |
| Link failure recover | + Simple                                                  | - Extra work required                                                  |
