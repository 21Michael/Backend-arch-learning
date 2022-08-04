# Asymmetric Encryption Methods
Asymmetric encryption is also known as **public key cryptography,** which is a relatively new method,
compared to symmetric encryption. Asymmetric encryption uses two keys to encrypt a plain text. 
Secret keys are exchanged over the Internet or a large network. It ensures that malicious persons
do not misuse the keys. It is important to note that anyone with a secret key can decrypt the 
message and this is why asymmetric encryption uses two related keys to boosting security. A 
public key is made freely available to anyone who might want to send you a message. The second 
private key is kept a secret so that you can only know.

A message that is encrypted using a public key can only be decrypted using a private key, while
also, a message encrypted using a private key can be decrypted using a public key. Security of
the public key is not required because it is publicly available and can be passed over the 
internet. Asymmetric key has a far better power in ensuring the security of information
transmitted during communication.

Asymmetric encryption is mostly used in day-to-day communication channels, especially over the
Internet. Popular asymmetric key encryption algorithm includes EIGamal, RSA, DSA, Elliptic curve
techniques, PKCS.

![link](https://www.ssl2buy.com/wiki/wp-content/uploads/2015/12/Asymmetric-Encryption.png)

## Pros:
  - ### No need for exchanging keys:
    In asymmetric or public key, cryptography there is no need for exchanging keys, thus
    eliminating the key distribution problem.
  - ### Increased security:
    The primary advantage of public-key cryptography is increased security: the
    private keys do not ever need to be transmitted or revealed to anyone.
  - ### Digital signatures:
    Can provide digital signatures that can be repudiated
## Cons:
  - ### Slow: 
    A disadvantage of using public-key cryptography for encryption is speed:
    there are popular secret-key encryption methods which are significantly faster
    than any currently available public-key encryption method.

## Algorithms:
![link](https://miro.medium.com/max/1400/1*lhIGfr01FCucZwwzRTTfMA.png)

## Conclusion:
Asymmetric cryptography is often used to check the authenticity of data using digital signatures.
A digital signature is a cryptographic technique for verifying the validity and credibility of a
message, software, or digital record. It’s the equivalent of an in-person signature or a sealed 
seal in digital form.

Digital signatures, which are based on asymmetric cryptography, may include proof of the origin,
identification, and status of an electronic record, transaction, or post, as well as acknowledge
the signer’s informed consent.

## Symmetric vs Asymmetric encryption:

|Key Differences|Symmetric Encryption|Asymmetric Encryption|
|---------------|--------------------|---------------------|
|**Size of cipher text**|	Smaller cipher text compares to original plain text file.|	Larger cipher text compares to original plain text file.|
|**Data size**|	Used to transmit big data.|	Used to transmit small data.|
|**Resource Utilization**|	Symmetric key encryption works on low usage of resources.|	Asymmetric encryption requires high consumption of resources.|
|**Key Lengths**|	128 or 256-bit key size.|	RSA 2048-bit or higher key size.|
|**Security**|	Less secured due to use a single key for encryption.|	Much safer as two keys are involved in encryption and decryption.|
|**Number of keys**|	Symmetric Encryption uses a single key for encryption and decryption.|	Asymmetric Encryption uses two keys for encryption and decryption|
|**Techniques**|	It is an old technique.|	It is a modern encryption technique.|
|**Confidentiality**|	A single key for encryption and decryption has chances of key compromised.|	Two keys separately made for encryption and decryption that removes the need to share a key.|
|**Speed**|	Symmetric encryption is fast technique|	Asymmetric encryption is slower in terms of speed.|
|**Algorithms**|	RC4, AES, DES, 3DES, and QUAD.|	RSA, Diffie-Hellman, ECC algorithms.|