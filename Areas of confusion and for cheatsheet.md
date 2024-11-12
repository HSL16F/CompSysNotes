Week 9 and UDP

Week 10: Three Way handshake, TCP protocol

Key to understand interfaces


Question about connection oriented an connectionless

Virtual circuits. Is it a mapping?

If used global name for virtual circuit it would be massive
For example, "Station St" that's generic, but if you know the suburb you understand the local area


![[Pasted image 20240531135725.png]]


### Random notes
Require the same protocols to communicate
Connection-less send and forget, no guarantee of delivery. Like texting or an API, you send the message, you don't know if it'll receive, each message is independent
Review of [[Protocol]]
End to end system review:
![[Pasted image 20240601090837.png]]

Two send data across a network, packets are the general term used.
Routers and link layer switches are two common packet switches

Each router has a forwarding table, IP addresses are hierarchical
```
forwarding table that maps destination addresses (or portions of the destination addresses) to that router’s outbound links. When a packet arrives at a router, the router examines the address and searches its forwarding table, using this destination address, to find the appropriate outbound link. The router then directs the packet to this outbound link.
```
The tables are generated via routing protocols

For persistent and non-persistent, whilst non-persistent has establishment at every point of connection, its advantage is that you can do it in parallel, say getting data from website, get images, text, and other files can get in parallel

HTTP is basically using a remote file system

![[Pasted image 20240602134046.png]]

Virtual Circuits
![[Pasted image 20240602135749.png]]
The 1 and 2 are virtual circuits. If you are travelling from H1 under VC 1, travel to C by 1, At C you come from A and travel to E, and at E, if come from C travel to F
The Virtual circuit is unique identifier. Can not issue to the same circuit to a different computer, as confuse/mess up the packets
VC is based on the router
New VC based on the forwarding table
![[Pasted image 20240602140140.png]]
Routing are predetermined in VC, unlike Datagram



