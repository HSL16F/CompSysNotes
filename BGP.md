Border Gateway Protocol is the "glue" which holds internet together, not perfect and based around manual oversite with peer and political restrictions.
Internet developed from independently administered networks, with Autonomous Systems (Group of routers under same admin control) and a network larger than all the IP addresses

Each network as a protocol for internal networking and protocol for external networking between AS's, this protocol must be the same for all AS's and is the purpose of BGP

Political considerations of BGP:
- Companies may not want other companies to use their network
- ISP's not want other ISP traffic on their network
- Desire to not carry commercial traffic on academic networks
- Switch to cheapest provider
- Don't send traffic through certain companies or countries
- Bellman's does not apply

BGP based on customer/provider agreement where customer pay for transit of traffic only they send or receive, not other's traffic or based on peering agreements where carry each other's traffic without charge
Provider advertises routes for entire internet, customer only advertise routs for their network to transmitting other traffic
![[Pasted image 20240531081551.png]]