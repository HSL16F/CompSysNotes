Focus on data plane vs control plane
Protocols don't have a single stack, BGP (Network layer) uses TCP (Transport layer) for updates
Different planes of protocols
- Data plane: Network layer: forwarding
- Control plane: Network layer: Choosing routs
- Management plane: Network layer: setting BGP policies
![[Pasted image 20240531164633.png]]
Protocols used at internet layer manage functionality, such as ICMP, DHCP and ARP
Other messages other than PING that the ICMP (Internet Control Message Protocol) can perform
![[Pasted image 20240531164645.png]]
Traceroute:
- TTL is hop count (Router the packet traverses)
- Traceroute sends out packets to same destination, each with incremented TTL
- Counters hit zero as successive routers causing router to return time exceeded message revealing IP address of router
- Sender can use information to determine path and timings of router a packet will take

Dynamic Host Configuration Protocol (DHCP):
Internet layers require host/interface to have a unique IP address, DHCP is a way to automatically deal with host allocation, though security concerns in connecting any device will issue IP address
The process of DHCP involves:
- Host broadcast DHCP DISCOVER packet using UDP from 0.0.0.0
	- Routers can be configured to relay DHCP server if not directly connected to same network
- DHCP Server receives request and responds with DHCP OFFER packet containing available IP address
- IP Addresses issues on a lease, time to use before server reclaim and re-issue IP address, a host can request a renewal before lease expires
Media Access Control (MAC) address is different to previously defined MAC, its set by the manufacturer and a hard-coded value, a 48-64 bits long. Used for DHCP server to know where to send the DHCP OFFER response to

Address Resolution Protocol:
ARP link between internet layer and network layer, translate IP into MAC
Broadcast arrive at every host in network and owner respond with MAC address, often used to figure out how to communicate with nearest router
ARP is very simple, not very efficient and many security problems
- No authentication
- Caching of responses when when not directly requested
- ARP spoofing often used to produce man-in-middle attack
- Provides way to intercept and spoof ARP messages to associate attackers address with another host IP address
