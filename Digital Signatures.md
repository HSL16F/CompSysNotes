Form of Asymmetric cryptography
- private signing key
- Public verification a key
Signature problem: Produce a signature for a message using signing key
s=sign(m, K_sign)
Verification algorithm:
- Verify signature via verification key, signature and original message
- verify(m, s, K_verification)
Provides both **integrity** and **non-repudiation** (Signer cannot deny signing the document)
Only B can sign using B's private signing key, only B has access to the key so it is therefore **non-repudiation**
Integrity is held as the original message is not altered

Digital Signature Protocol:
A generate signature message for m, s=sign(m, KA_sign)
A send m and s to B
B accept m IFF verify(m,s,KA_verification) is successful

Message not confidential, sent in plaintext, goal to detect modification
For large messages, hashing can be applied to generate hash H(m) which is signed and verified
Protocol:
A generate signature s=sign(H(m), KA_sign)
A send m and s to B
B generate H(m) and accept m IFF verify(H(m),s,KA_verification) is successful