![[Pasted image 20240529221427.png]]
Client: Browser with access to pages
Server: Daemon based on content delivery of pages
URL is Protocol +[[DNS|DNS name]] + file name
URL is Uniform Resource Locator, can be
	absolute: “http://www.google.com”
	relative:   “./nextpage.html"
Differs from Uniform Resource Identifier (URI)

The general scheme of what a URL looks like is as follows:
scheme:\[//\[user\[:password]@]host\[:port]]\[/path]\[?query]\[#fragment]
abc://user:\passwd\@example.com:80/dir/file.html?key=value#result
key and value is to find files.
HTTP and internet is all just files but remotely, though scheme above is no longer common

Overview of protocol:
- Client initiate TCP connection (Create socket) default port 80
- Server accept TCP connection from client
- HTTP message at application layer protocol message exchanged between HTTP client and HTTP server
- TCP closed
Note that HTTP 1.0 single-use connection, 1.1 uses persistent connections and additional headers

Map diagrams via a zigzag diagram
**Persistent vs Non-Persistent**
Persistent:
- Server leaves connection open after sending response, it always listening
- Following HTTP messages between same client/server sent over open connection
- Client sends requests as soon as it encounters references object, this reduced overall response time
- You keep the data open and get the data as you want, total work is done less, but don't hog as much 
Non-persistent:
- Requires 2 "response time", one to initiate TCP connection and one for initial HTTP request per object and file transfer time. Remember to factor in the request to open the connection before sending files
- OS overhead for each TCP connection
- Browser often open parallel TCP connections to fetch references objects, makes it very efficient to get data with hogging more data

The following steps occur when HTTP link is selected:
Browser determine URL->Browser make TCP connection->Send HTTP request response->Browser fetch other URL's as needed and may open more TCP->browser display page and more content as it arrives->TCP connections released/closed after content sent

Various HTTP requests:
![[Pasted image 20240530081030.png]]
Note that safe implies only information retrieval and does not change the state
Idempotent implies multiple identical requests have the same affect. You GET same thing, still same outcome, you DELETE and its already deleted, still try to DELETE. Anything if you do something twice

#### Requests
Example of request with request line (GET, POST, HEAD) and various header lines
Blank lines (2 CR/LF) indicated end of message
GET /somedir/page.html HTTP/1.1  
Host: www.somesite.com.au  
User-agent: Mozilla/4.0  
Connection: close  
Accept-language: fr

Response:
HTTP/1.1 200 OK  <- Status line (Protocol, status code and phrase)
Connection: close  
Date: Thu, 06 Aug 2009 12:00:15 GMT  
Server: Apache/2.2.11 (Unix)  
Last-modified: Mon, 22 Jun 2009  
Content-Length: 6821  
Content-Type: text/html

`<html><some more data>...`

Host through to Accept-Language is part of the header, anything but html
There can be several status code and responses
![[Pasted image 20240530081458.png]]
404 is page doesn't exist
HTTP and HTTPS different

There can be a large variety of header types
Some can be request type, others response type with some both
![[Pasted image 20240530081806.png]]
![[Pasted image 20240530081822.png]]
Cookies quite important, persistent wait till download all. Cookie knows its the same transaction.

There's HTTP 2 and 3 which differ by utilisation of say [[Multiplexing|multiplexing]] and decreases latency 
HTTPS is HTTP over TLS, not a different protocol but HTTP over a different service and uses port 443 instead of port 80. Everything in encrypted with HTTPS over HTTP where just the payloads are encrypted
