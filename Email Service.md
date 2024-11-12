Email Service are based on two RFC standards. RFC 2821 (transmission) and RFC 2822 (Message format)
The architecture and services involve:
- User agents (UA's and MUA's) which allow a user to read and send email
- Message Transfer Agents (MTA's) which transport a message from source->destination
![[Pasted image 20240526162101.png]]

### User Agents
Serve to compose, report, display and dispose emails
Envelop and contents: Encapsulation of transport related information
Header: User agent control info
Body: For human recipient not meant for machine reading
User provides message, destination, optional other params
Addressing scheme user@dns-address
![[Pasted image 20240526162351.png]]

### Simple Message Transfer Protocol: SMTP
SMTP uses TCP to transfer email message from client to server via default port 25. Typical direct transfer, sending server to receiving server. Three phases involved:
- Handshake (greeting)->Transfer message->Closure
Command/response interaction: Commands in ASCII text and response consists of Status code and phrase. Messages must be in 7-bit ASCII
TCP is analogous to HTTP
SMTP is very chatty with many interactions

### Multipurpose Internet Mail Extensions: MIME
Used for only English and ASCII. Other language requirements needed and other message content type such as audio/images was needed. MIME has 5 additional header information
- MIME-Version: Identify MIME version
- Content-Description: Human readable description of contents
- Content-ID: Unique identifier
- Content-Transfer-Encoding: How body is wrapped for transmission
- Content-Type: Type and format of content
#### Message Transfer and Access
Transfer:
SMTPL delivery/storage to receiver's sever
Delivery:
- Local, Pop3, IMAP and HTTP

**Receiving local vs remote:**
![[Pasted image 20240526163649.png]]
In the fist one, sending and reading mail when receiver has permanent internet connection and the UA runs on same machine as the transfer agent. In the second, the computer (User's PC), it is separate which his far more comment these days. Not on the same network.

### Internet Message Access Protocol: IMAP
IMAP allows users to query MTA, it allows user state across sessions:
- Retain mailbox contents and allow manipulation of online and offline messages and mailbox folders
- Supports high volume of IMPA servers and limited by size of storage as retains mailbox contents online on a server
