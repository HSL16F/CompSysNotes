Each router as forwarding/routing table
Maps destinations addresses to outgoing interfaces
When a packet is received
- Assess destination IP address in header
- Index at table
- Determine outgoing interface
- Forward packet to next interface
Router path repeats process. Point to point communication
![[Pasted image 20240530232924.png]]Tables are developed via [[Routing Algorithm|routing algorithm]]. Mixture of
- local algo for reach router
- Protocol to gather network information needed for algo
