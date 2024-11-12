ECB or Electronic Codebook and CBC or Cipher Block Chaining are two operations
## ECB
Each block is encrypted and decrypted independently using K_s
![[Pasted image 20240520214447.png]]
Both encryption and decryption are parallelisable but typically should not be used, same text ALWAYS encrypts two the same cipher therefore can determine the encryption, leaks information about the plaintext. Identical plaintext blocks have identical ciphertext blocks therefore identical message result in identical ciphertexts
![[Pasted image 20240520214859.png]]
## CBC
More advanced based on probabilistic encryption, identical plaintext will *most likely* result in different ciphertext. Randomness applied via an initialisation vector (IV) which MUST BE RANDOM AND NOT RESUED and does not necessarily be a secret
Encryption follows the process of:
First block with an XOR plaintext and IV, encrypt->ciphertext, other blocks XOR previous ciphertext with plaintext , encrypt->ciphertext
Decryption follows the process of:
First block decrypt cipher text and XOR with IV->plaintext, other blocks decrypt ciphertext and XOR with previous ciphertext->plaintext
![[Pasted image 20240520215450.png]]
CBC does not support parallelism, CBC must be performed sequentially, encrypting block requires n-1 block to be encrypted
Decryption can be performed in parallel, no need to decrypt n-1 block before decrypting block n

Loss/corruption of a ciphertext blocks affects decryption for up to 2 blocks
![[Pasted image 20240520220002.png]]
