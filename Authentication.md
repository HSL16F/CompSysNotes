Authentication encryption provides both confidential, encrypt via [[MAC]]
Protocol:
A generate c=encrypt(m, Kenc_Secret)
A generate tag t=mac(c, Kmac_secret)
A send c and t to B
B generate tag for c, t'mac(c, Kmac_secret)
If t=t' then m=decretpy(c,Kenc_secret) else message has been tampered
Examples of this include AES-GCM, AES-OCB and AES-CCM
![[Pasted image 20240521173804.png]]
Encrypt then MAC is a symmetric cryptosystem, relied on shared keys which are securely exchanged
Shared secret keys to encrypt/decrypt and one to generate MAC tags
Apply asymmetric encryption protocol for such tasks but must ensure authentication
![[Pasted image 20240521173959.png]]
Issue of ensuring that B is the owner of the public key, this is achieved via [[Certificates]]