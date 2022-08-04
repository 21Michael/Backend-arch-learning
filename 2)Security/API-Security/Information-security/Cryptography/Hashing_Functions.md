# Hashing Functions

**A hash function** is a versatile one-way cryptographic algorithm that maps an input of any size to 
a unique output of a fixed length of bits. The resulting output, which is known as a hash digest,
hash value, or hash code, is the resulting unique identifier.

A hash function takes a group of characters (called a key) and maps it to a value of a certain 
length (called a hash value or hash). The hash value is representative of the original string of 
characters, but is normally smaller than the original.

Hashing is done for indexing and locating items in databases because it is easier to find the
shorter hash value than the longer string. Hashing is also used in encryption.

![link](https://www.thesslstore.com/blog/wp-content/uploads/2018/12/Hashing-Example.png)

## Pros:
  - ### Determinism
    A hash algorithm should be deterministic, meaning that it always gives you an output of 
    identical size regardless of the size of the input you started with. This means that if you’re
    hashing a single sentence, the resulting output should be the same size as one you’d get when
    hashing an entire book.
  - ### Pre-Image Resistance (one-way encrypting)
    The idea here is that a strong hash algorithm is one that’s preimage resistance, meaning that
    it’s infeasible to reverse a hash value to recover the original input plaintext message. 
    Hence, the concept of hashes being irreversible, one-way functions.
  - ### Avalanche Effect 
    What this means is that any change made to an input, no matter how small, will result in a 
    massive change in the output. Essentially, a small change (such as adding a comma) snowballs
    into something much larger, hence the term “avalanche effect.”
  - ### Hash Speed
    Hash algorithms should operate at a reasonable speed. In many situations, hashing algorithms
    should compute hash values quickly; this is considered an ideal property of a cryptographic
    hash function. However, this property is a little more subjective. You see, faster isn’t 
    always better because the speed should depend on how the hashing algorithm is going to be 
    used. Sometimes, you want a faster hashing algorithm, and other times it’s better to use a
    slower one that takes more time to run through. The former is better for website connections
    and the latter is better for password hashing.
  - ### Collision Resistance
    This property means it should be hard to find two different inputs of any length that result
    in the same hash. This property is also referred to as collision free hash function.

## Algorithms:
![link](https://d3i71xaburhd42.cloudfront.net/e2917caeddacb7807af75dcf1d1bc44fd965316e/2-Table2-1.png)

## Conclusion:
One purpose of a hash function in cryptography is to take a plaintext input and generate a 
hashed value output of a specific size in a way that can’t be reversed. But they do more than 
that from a 10,000-foot perspective. You see, hash functions tend to wear a few hats in the 
world of cryptography. 

**In a nutshell, strong hash functions:**
  - **Ensure data integrity;**
    ![link](https://www.thesslstore.com/blog/wp-content/uploads/2021/01/hashing-email-example.png)
  - **Secure against unauthorized modifications;**
  - **Protect stored passwords;**
  - **Operate at different speeds to suit different purposes;**