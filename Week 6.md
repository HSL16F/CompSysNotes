Introducing networks, protocols and OSI layers
The internet is described as a network of networks, its an aggregation of many smaller networks and is not under a single point of control.
3 phases of internet. ARPANET, NSFNET and Internet
Sample of structure of the internet
![[Pasted image 20240524233816.png]]
#### Properties and Complexity of internet
- Internet connections millions of nodes, often no direct physical connections between most pairs
- Internet tells data where to go
- Must specify where physical signals are to be sent and physical links between different pairs must exist
- Important to have modular way to handle tasks separately

### Networks
[[Networks and layers]] have various layers and models as well as notes on network architecture
There are two main versions of connections
[[Connection-Oriented]] and [[Connectionless]] services. The choice of which service to use depends on reliability, quality and cost of service. Both have pro's and con's depending on circumstances
There are two standard sets of layers
- #### [[TCP IP]]
- #### [[OSI]]
The mapping of protocols around TCP/IP to the OSI model, various protocols straddle layers and there can be some ambiguity to which layer a protocol belongs to
Comparison of layering of TCP and OSI
![[Pasted image 20240525112653.png]]
Protocols often involve layering of encapsulation
![[Pasted image 20240525112739.png]]
Packets are often grouped together

The protocol stacked is as featured below
![[Pasted image 20240525112823.png]]
Though focus is on top three layers, application layer, TCP, UDP and IP
