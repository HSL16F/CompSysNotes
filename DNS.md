Domain Name Service maps names to numbers. It maps human-readable names to computer friendly IP addresses

Domains include:
- facebook.com
- unimelb.edu.au
- student.unimelb.edu.au
Sockets require IP addresses such as
- 128.250.81.2
- fe80::69a4:1496:4354:1862
The DNS operates in the application layer has to create a socket to find out the IP address, it must work with a hard-coded IP address to open up its socket

Elements which comprise the DNS:
- [[Domain Name Space]]: DNS uses a tree structure name space to identify resources on the internet
- [[DNS database]]: Each node/leaf in the name space tree names a set of information which contains a resource record (RR). The collection of all RR's is organised via a distributed DB
- [[Name servers]]: Server programs which hold information about a portion of the domain name tree structure and the associated RR's
- [[Resolves]]: Programs who extract information from name servers in response to client requests
