Message Authentication Code is used to detect if a message has been tampered with, requires a shared secret key
Mac function generates some tag t given message and a secret key, for example, t=mac(m, K_s)
Common to apply a hash function to take as input for the secret key and the message concatenated
![[Pasted image 20240521171748.png]]
A and B have shared secret key K_s and to verify a message, the protocol/exchange proceeds as follows:
A generate message to B
A generate tag t=mac(m, K_s)
A send m and t to B
B calculate t'=mac(m,K_s)
B verify t=t', if true than m has not been altered, if t!=t' then m has been tampered
m is in plaintext, goal not for confidentiality, but instead to detect modification
![[Pasted image 20240521172025.png]]
