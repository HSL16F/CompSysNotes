Example of a protocol stack
Networks are often modelled as a stack of layers, each layer offers services to the layer ABOVE it and inter-layer exchanges are conducted according to some [[Protocol|protocol]]
![[Pasted image 20240524234639.png]]
Services to protocols relationships includes for example
![[Pasted image 20240524234704.png]]
**Definitions:**
- Services are defined as a set of primitives that a given layer provides to a layer above it. It acts as an interface between the layers
- Protocols informally defined as rules which govern format and meaning of packets that are exchanged by peers within a given layer, that is packets sent between peer entities
Protocol Stack
![[Pasted image 20240525112835.png]]
Note that one network *can* support multiple network layer protocols

#### Network architecture
The narrow waste design of [[TCP IP]] is part of the architecture of the network
- Design decisions that go beyond individual layers
- They are often hard to change and important to make the right decisions early on
- However if too complicated and ideal, there's risk of stagnation for example [[OSI]]
TCP/IP is simple, small and flexible. TCP+IP can be used on a single layer
There is a change occurring where HTTP is almost becoming the *new* narrow waist
![[Pasted image 20240525113410.png]]

### Client Server definition
In an example of a phone call:
Receiver:
- Ensures SIM card is in, Phone is on, phone not in aeroplane mode
- Is READY to accept a call from anyone
Caller:
- Same checks and conditions as above
- Dial number to say "WHO" you want to connect to
After both sides can talk and listen equally
The definition of Client and the Server is some what arbitrary and depends on the general state.
![[Pasted image 20240526110158.png]]