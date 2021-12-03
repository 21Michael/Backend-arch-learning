# Symmetric Encryption Methods
This is the simplest kind of encryption that involves only **one secret key** to cipher and decipher
information. Symmetric encryption is an old and best-known technique. It uses a secret key that can
either be a number, a word or a string of random letters. It is a blended with the plain text of a
message to change the content in a particular way. The sender and the recipient should know the 
secret key that is used to encrypt and decrypt all the messages. Blowfish, AES, RC4, DES, RC5, 
and RC6 are examples of symmetric encryption. The most widely used symmetric algorithm is AES-128,
AES-192, and AES-256.

![link](https://www.ssl2buy.com/wiki/wp-content/uploads/2015/12/Symmetric-Encryption.png)

## Pros:
  - ### Extremely Secure 256-bit key length algorithms:
    When it uses a secure algorithm, symmetric key encryption can be extemely secure. One of the
    most widely-used symmetric key encryption systems is the U.S. Government-designated Advanced
    Encryption Standard. When you use it with its most secure 256-bit key length, it would take 
    about a billion years for a 10 petaflop computer to guess the key through a brute-force attack.
    Since, as of November 2012, the fastest computer in the world runs at 17 petaflops, 256-bit
    AES is essentially unbreakable.
  - ### Relatively Fast:
    One of the drawbacks to public key encryption systems is that they need relatively complicated
    mathematics to work, making them very computationally intensive. Encrypting and decrypting 
    symmetric key data is relatively easy to do, giving you very good reading and writing 
    performance. In fact, many solid state drives, which are typically extremely fast, use 
    symmetric key encryption internally to store data and they are still faster than unencrypted
    traditional hard drives.

## Cons:
  - ### Sharing the Key:
    The biggest problem with symmetric key encryption is that you need to have a way to get the 
    key to the party with whom you are sharing data. Encryption keys aren't simple strings of
    text like passwords. They are essentially blocks of gibberish. As such, you'll need to have 
    a safe way to get the key to the other party. Of course, if you have a safe way to share the
    key, you probably don't need to be using encryption in the first place. With this in mind, 
    symmetric key encryption is particularly useful when encrypting your own information as 
    opposed to when sharing encrypted information.
  - ### More Damage if Compromised:
    When someone gets their hands on a symmetric key, they can decrypt everything encrypted with
    that key. When you're using symmetric encryption for two-way communications, this means that 
    both sides of the conversation get compromised. With asymmetrical public-key encryption, 
    someone that gets your private key can decrypt messages sent to you, but can't decrypt what 
    you send to the other party, since that is encrypted with a different key pair.

## Algorithms:
![link](https://d3i71xaburhd42.cloudfront.net/900e50417464460abe15410831b1cf51c0afc5f3/4-Table1-1.png)

## Conclusion:
Although symmetric encryption is an older type of encryption, it is simpler and more effective 
than asymmetric encryption, which strains networks due to data size performance problems and 
heavy CPU usage.

Since symmetric encryption performs smoother and quicker than asymmetric encryption, it is 
commonly used for bulk encryption / encrypting massive volumes of data, such as database 
encryption. In a database, the secret key can be used only by the database to encrypt or 
decrypt data.

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