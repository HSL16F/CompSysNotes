Properties of a good routing algorithm
- Correctness
	- Find valid route between all pairs of nodes
- Simplicity
- Robustness
	- Router crash should not affect all of network
- Stability
	- Reaches equilibrium and say there until conditions change
- Fairness
- Efficiency
- Flexibility to implement policies

**Delay Bandwidth tradeoff:**
Mean packet delay or Max network throughput
Goal to minimise number of hops each packet makes and actual algorithms provide cost for each link
- Reduce per packet bandwidth and improve delay
- Hopefully reduces distance travelled but not guaranteed (Example cross ocean is one IP hop)
- Cost of each link lead to more flexible but cannot express all routing preferences (No global view)

### Adaptive Routing Algorithms
Two sets of routing Algorithms
Static/Non-adaptive Routing:
- No adaption to network topology
- Calculated offline and uploaded to router at boot hence little response to failure
- Useful for when the network will rarely change, such as home router will have static route, you only always connect to the one router
Adaptive:
- Dynamic routing, adapts to changes in topology and sometimes traffic levels conditional on sophistication
- Optimise some measure such as distance, hops, estimated transit time
- Can retrieve information from adjacent routers or from wider network

#### Flooding
Flooding is the simplest approach to adaptive routing
- Forward to ALL of neighbours
- Guarantee shortest distance and minimal delay
- Used to benchmark speed
- Creates many duplicate packets
- Important to have a way of discarding packets, when unknown, set to diameter of network
![[Pasted image 20240531072413.png]]

#### (Bellman) Optimality Principle
If router J is on optimal path from I to K, then J and K also fall on optimal path, though this case does NOT always apply
Set of optimal routes is tree with root from destination
![[Pasted image 20240531072609.png]]

#### Dijkstra's
For finding shortest path when weights are provided. Nodes divided up into unseen, open and closed
Open is aware of path, but may not be best path. Closed IS best path, set all noes to unseen (Not neighbour)
See slides for example
![[Pasted image 20240531072915.png]]
Note shortest path from A->D follow along H

#### Link State Routing
Distributed algorithmic with 5 steps
- Discover neighbours and learn their network address
- Set distance/cost metric to each of neighbours
- Construct packet containing all learnt
- Send packet to and receive from all other routers
- Compute shortest path at every other router
Send out HELLO packet on each interface, router return with same unique ID
The cost can be set automatically, generally set with 1/bandwidth, so 1Gbps=1, 100Mbps=10
![[Pasted image 20240531074349.png]]
Flooding is used to send packets to all other routers. Flooding uses acknowledgements to guarantee all other router receives packet. To prevent waste, when router receives Link State Packet, compare sequence number to one previously received (If received any) and if sequence number not larger, it discard and do not forward in flood
Sequence numbers are 32bits to avoid wrap-around, though still possible, but if router crashes, start its sequence number from 0. The age of the field is reduced by 1 each second and when age hits 0, information is discarded, its possible for wrap-around but very unlikely
