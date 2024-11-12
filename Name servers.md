Various [[Domain Name Space]] can be grouped via zones
![[Pasted image 20240526155124.png]]
DNS names are divided into overlapping zones. The name servers are authoritative for a given zone. usually two name servers for a zone.
Name servers are arranged in a hierarchical manner which extends from the root servers
Root name servers are form the authoritative cluster for enquiries. Root servers are contacted by a local name server that cannot resolve name

There are various types of TLD DNS servers responsible for com, org, net, edu etc and all top level country domains such as uk, au, jp such as network solutions maintains servers for com
There exist various authoritative DNS server organisations such as DNS servers providing authoritative hostname to IP mappings. These can be maintained by the organisation itself or a service provider.
Its typical for each ISP (Residential ISP, Company, University etc) to have a default name server to handle DNS queries. It returns a cached value if one exists, else acts as proxy and forwards the request up the query hierarchy.
