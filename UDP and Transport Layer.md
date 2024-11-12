User Datagram Protocol or UDP acts at the transport layer, an extension of [[Socket|sockets]]
[[Networks and layers|Transport Layer]] provides services to applications by the network layer
Application needs:
- Data from one application which is not altered/mixed with another application
- Data doesn't arrive faster than we can handle
- Data is stream of bytes
- Data arrives reliably and know when packets are lost
- Data arrives in generally order
Network provides:
- Packets form host to host

UDP allows for the transmission of datagrams over IP without a connection, therefore connectionless. UDP transmits segments consisting of header followed by payload. Headers contain the source and destination ports with a UDP socket with 3-tuple and each packet containing 5-tuple. Payload is handed process which is attached to particular port as destination.
Each message is carried independently, first message to a well-known port from a dynamic port, server replies from well-known port to save dynamic port. Client uses same ports
![[Pasted image 20240530193648.png]]
UDP is simple and efficient, it is suitable for when:
- Client sends short request to server and short response expected, if request or response lost, client timeout and resent request
- UDP has simple code and fewer messages, one in each direction. [[DNS]] is an example of suitable application and real-time services due to packet lost, don't wait for it to resend, move on and can conceal lost, voice and video you can deal with minor drops in communication
Pro's and con's of UDP:
- Pro: Multiplexing leads to no delay to recover lost packets
- Con: No flow and error control, retransmission of bad segments
UDP suitable for when precise control over packet flow/error/timing is where UDP shines best

The transport layer services provide interfaces between the application layer and the network/internet layer. Services are logical communication channel's between processes running on different hosts.
[[Connection-Oriented]]:
- Connection establishment, data transfer, connection release (TCP) and thought of like a call
[[Connectionless]]:
- More similar to text messages, UDP is an example of connectionless

The transport service provides [[Multiplexing|multiplexing]] and provides a reliable service on top of an unreliable network
![[Pasted image 20240530172438.png]]
Packets name differ in meaning depending layer, but packets can generally referred as packets at all layers for simplicity.
[[Multiplexing]] is useful for an unreliable connectionless service
Regarding a reliable connection oriented service:
- Provide notion of "perfect" connection between two nodes which
Abstraction representation of a message to and from transport entities, the message is encapsulated within segments referred to as transport layer units within packets which are further encapsulated within frames.
![[Pasted image 20240530191203.png]]

#### Addressing in Transport Layer
Remote process to connect to is required at both application and transport layer. At the transport layer, this is achieved via port numbers, such as port 80
The full address is a 5 tuple, though typically to only have 3 tuple of LocalIP/Port
Full address: Protocol, Local IP, Local port, remote IP, remote port

Port numbers are assigned by an authority. Well known ports range from 0-1023, such as SSH (22), and HTTP (80)
1024-49151 are registered ports, though ports have 2^16 bit range, >49151 is dynamic ports
![[Pasted image 20240530192059.png]]
