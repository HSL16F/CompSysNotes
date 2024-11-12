A sock is defined how a user-space code sends messages to the kernel-space networking code.
The process sends and receives through a socket where a doorway leads in/out of the application
![[Pasted image 20240526105025.png]]
![[Pasted image 20240526105058.png]]

Sockets involve a 5-tuple:
- Protocol
- Local-IP
- Local-port-number
- Remote-IP
- remote-port Number
This is typically referred to as the source and dest (Destination) not local and remote
![[Pasted image 20240526105429.png]]

Most major OS's use the Berkeley socket UNIX for their socket interface which are quite portable
UNIX treats everything like a file, so input is like reading a file, output is writing a file and a file is addresses by an integer file descriptor
API implements system calls such as connect(), read(), write() and close()

The difference between a client and a server is simply defined by the [[Networks and layers|Receiver and the Caller]].
![[Pasted image 20240526110201.png]]

#### Socket Primitives
SOCKET: Creates new communication endpoint
BIND: Associate a local address with a socket
LISTEN: Announce willingness to accept connections; give queue size
ACCEPT: Passively establish an incoming connection (Block until then)
CONNECT: Actively attempt to establish a connection
SEND: Send some data over a connect via write()
RECEIVE: Receive some data from the connection via read()
CLOSE: Release the connection

A state diagram can be used to express connections and state flow/movement
![[Pasted image 20240526112945.png]]

Based on code expressed in Week 7 content:
A server has two sockets, listendf, and connfd
Listening sock as a half socket, it contains a 3-tuple of the:
- Protocol
- Local IP Address
- Local Port Number
It can be thought of as a receptionist or the automated "Press 1 for..."
It waits f or calls and puts them through to another line via connfd
Connection socket is a type of socket where read/write operations are possible which contains the 5-tuple

There also exists Blocking and non blocking reads:
Reading from a stored file is always data to read until EOF (End of file)
When over a network, data arrives in stages so careful to ensure if been reading was less then what was in the write() call

TLS also known as Secure Socket Layer is a [[Protocol]] designed for sockets to carry plain text
An extra handshake is needed at the beginning to verify and set up a cryptographic exchange. It is somewhat similar to [[TCP IP]] however slightly more secure
![[Pasted image 20240526113549.png]]
TLS is simple to use for encryption and needs to provide identity verification which is harder
TLS creates a data pipe between two hosts.
Note that most of the TLS content is assumed to be related to Assignment 2 which is not relevant for the exam so less focus was placed on it for notes.