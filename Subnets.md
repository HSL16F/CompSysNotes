Prefixes in IP addressing indicate different destination networks, this can be used within a given organisation via a subnet mask.
Subnetting splits a network into several parts for internal use while acting as a single network externally
Subnet marks written same as a network mask

Example of subnets:
- Packets arrive over the internet
- Router use subnet mask (bitwise AND) to find correct subnet to send packet to without knowing all hosts of subnet
![[Pasted image 20240531161410.png]]
![[Pasted image 20240531161437.png]]
![[Pasted image 20240531161747.png]]
Future changes can be made without external impact as there's no need to request additional IP address's and routing to the internet does not change, only internally. The internet isn't just a network of networks, but a hierarchy of networks of networks
![[Pasted image 20240531162713.png]]
![[Pasted image 20240531162825.png]]
Each link is a subnet
4 networks with uses and 3 joining networks of routers
Divided /24 into four /26 subnets one for each network, /24 is 256 addresses
![[Pasted image 20240531163159.png]]
![[Pasted image 20240531163217.png]]
![[Pasted image 20240531163246.png]]
![[Pasted image 20240531163304.png]]
Routing table via merging prefixes
![[Pasted image 20240531163320.png]]
![[Pasted image 20240531163340.png]]
