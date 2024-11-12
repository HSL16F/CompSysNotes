Provides Confidentiality
Have plaintext->encrypt into criphertext so only authorised parties know how to decrypt the cipher text-> into plaintext
c=encrypt(m, k_e) encrypts the message m (plaintext) using encryption key k_e
m=decrypt(c, k_d) decrypts the ciphertext c using decryption key k_d
The content of the message MUST be hidden from all but those holding k_d

**Kerckhoff's Principle** states that secrecy should depend only on decryption key remaining secret and that secrecy should not depend on the algorithm to remain secret. For example, RSA algorithm is known, but the output is not known.

![[Pasted image 20240520182530.png]]

There's two variants of encryption Symmetric and Asymmetric
#### Symmetric
Uses same key for both encryption and decryption, key must remain secret
c=encrypt(m, k_s), m=decrypt(c, k_s), K_s should be securely exchanged between the communication parties, modern example is AES
An example of a symmetric encryption protocol:
A and B secure exchange with K_s
A compute ciphertext c with encrypt(m,K_s)
A->B
B recover m compute decrypt (c, K_s)
AES is a block cipher to ensure that K_s is secure and confidential. AES breaks data into fixed sized blocks and encrypt/decrypt each block
Note though that AES and block ciphers have different modes of operation which determine how each block is treated/linked
ECBE or Electronic Codebook and CBC or Cipher Block Chaining are two operations
[[Block Cipher]]
#### Asymmetric
Use two different keys, public to encrypt and a private key to decrypt, only private key must remain secret
Public keys are known, private are not. All principals (users such as Alice and Bob) have pairs of keys, public and private, encryption performed by public key, decryption via private which is only accessible from owner of the key pair
Process involves:
B generate key pair of KB_public, KB_private, KB_public posted online
A access KB_Public and compute ciphertext c via encrypt(m, KB_public)
A send c to B
B recover m via decrypt(m, KB_private)
No need to securely exchange any keys
Asymmetric whilst good, is limited with large messages as it is rather inefficient

#### Hybrid Encryption
Bridge between best of both worlds
Symmetric encryption is efficient for large messages but requires securely exchanging secret key
Asymmetric doesn't need a secure exchange but not efficient for large messages
Hybrid uses encryption to secure exchange of a shared secret key (Like asymm) and use encryption to encrypt communication of messages with a shared key like symm
Typical protocol is as follows:
A generate keypair (KA_public, KA_private)
A post KA_public->B take KA_public
B generate K_secret
B compute cipher text with secret key c=encrypt(K_secret, KA_public)
B send c to A
A recover K_secret by computing decrypt(c, KA_private)
A, B share secret key and can exchange messages via symmetric encryption
