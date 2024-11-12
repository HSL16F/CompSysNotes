Transmission Control Protocol/Internet Protocol or TCP/IP model reflects what occurs in practice on the internet.
It was designed to  be independent of data link and physical layers
IP acts like a narrow waste, many application protocols, one network protocol (IP) and many link layer protocols
IP over everything and everything over IP
If a new physical supports IP, then it supports everything, if the application runs on IP, it runs over everything
SMS and voice calls run in non-IP networks, and one network can support multiple network layer protocols

TCP transmits steams of bytes without concern for
- Segmenting into IP Datagrams->Stream oriented
- Bytes dropped or duplicated->reliable
- Bytes arriving out of order->in order
TCP transport entity manages TCP streams and interfaces to IP layer, recipient TCP entities reconstruct original byte streams from encapsulation.

Primitives are core functions which allow interfaces with transport services such as TCP:
![[Pasted image 20240530203645.png]]
TCP Connections are:
- Full duplex: Data in both directions simultaneously
- End to end: Exact pairs of senders and receivers
- Byte Streams not message streams which implies
	- Application layer messages boundaries are not preserves
	- You can't tell where one write ends and another begins
- Buffer capable
	- TCP entity can choose to buffer prior to sending or not
	- Buffering reduces overhead (Fewer headers) but increases delay

Example of byte stream model:
![[Pasted image 20240530204140.png]]
Read() can read parts of segments, parts of write()'s multiple segments or multiple write()'s

**TCP Properties**
Data exchanged between TCP entities in segments, each has 20-60 byte header with zero or more data bytes (You can have just a header with no data)
TCP entities decide how large segments should be given IP payload <65,515 (2^16-20-1)
Maximum Transfer Unit (MTU) is around 1500 bytes
Sliding window protocol
- For reliable data delivery without overloading receiver and now used with congestion control

### TCP Header
![[Pasted image 20240530204714.png]]
Important header fields
![[Pasted image 20240530204738.png]]

As TCP is a [[Connection-Oriented]] protocol running over a connectionless network later of IP, its important to consider when a network looses, store or duplicate packets.
- Congested networks may delay acknowledgements
- Incurring repeated multiple transmissions
- Any that have not arrived or are out of sequence lead to delayed duplicates

### Three way handshake
The three way handshake was established for reliable connection
- Ensures only one connection is established, even if some set up packets are lost or transmitted
- Establish initial sequence numbers for sliding window and negotiate params
The sender receiver exchange information about which sequencing strategy each will use, an agreement is made and then transmission of segments occurs.

Synchronisation is very important for connections:
SYN and FIN count for 1 byte in sequence number and the sequence number of the first data byte is seq num of SYN+1
Sequence number is the first byte of a given segments payload, its offset by a random number, initial value is somewhat arbitrary and offset is reflected in both sequence and acknowledgement numbers.
Acknowledgement number is the next byte sender expects to receive. Bytes received without gaps, a missing segment will stop incrementing, even if later segments have received
![[Pasted image 20240530210908.png]]

SYN bit used to establish connection, connection request is SYN=1, ACK=0, connection reply is SYN=1, ACK=1
SYN used in both CONNECTION_REQUEST and CONNECTION_ACCEPTED, distinguishes them
To close TCP, FIN flag is used. FIN is directional, once acknowledged, no new data can be sent from sender to receiver. Data can flow in the other direction, but the other party will stop listening, sender can still retransmit unacknowledged segments
Typically requires 4 segments to close, 1 FIN, 1 ACK for both parties.
RST flags are used to hard close a connection without a acknowledgment. Close connection and do not listen to nay more, sent in reply packet of 5 tuple with no open connection

SYN flooding old method where attacker make initial SYN request and not reply with ACK therefore filling up server queue with sequence numbers for defunct connections
SYN cookies used to solve this, they are slower, and incur performance cost of validating SYN cookies, but typically only used when server believes to be under attack
