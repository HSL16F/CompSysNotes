Purpose of integrity
- Verify a message has not been tampered with
- Prevent attacker can read, modify and delete messages
Two approaches to ensure integrity
- ### [[MAC]]
- ### [[Digital Signatures]]
### Cryptographic Hashing
Important to understand for integrity measures
A hash function takes an arbitrary length input m and produced fixed length hash or digest H(m)
Two critical properties are:
- Collison resistance
	- It is hard to find that for some m!=m'->H(m)=H(m'), that is VERY rarely does two different messages produce the same Hash
- One way
	- It is very difficult to find m given H(m)

![[Pasted image 20240521140318.png]]
