Digital Certificates secure associate identities with cryptographic public keys, digital cert is a signature which binds identity of principal and public key of principal (Encryption or verification key)
Given issue with key pair KIssuer_public and KIssuer_private, a given principal's identity B and public key KB_public the following is established
- binding = B, KB_public
- Signature = sign(binding, KIssuer_private)
- certificate(B, issuer)=(binding, signature)
Issuer is certifying that KB_public belongs to B
Protocol to verify that B is the correct identity and corresponding public key
B create message m
B sign S_m=sign(m, KB_private)
B send m, s_m, certificate(B,issuer) to A
A verify cert via verifying signature verify(binding, signature, kissuer_public) and verify identity of binding corresponds to B's identity
If verification successful, A retrieve KB_public from cert and only accept if verify(m, s_m, KB_public) succeeds

Certificate authorities are authorities sources which are trusted, this ensures that Kissuer_public can be trusted
They sign certs for others, public keys are contained in root certs that are self-signed, root certs are shipped, pre-loaded with OS and browsers