# Injected client + interception (HMAC signature)

## Preventing mechanisms:
  - ### MAC 
    **MAC (Message Authentication Code)**
    It is a small piece of information that helps to authenticate a message. 
    Moreover, it ensures that the message came from the stated sender. The MAC 
    value protects both a message’s data integrity and its authenticity.
    It helps to figure out any changes to the message content.  
    --  
    A MAC code is calculated by using a message and a secret key as inputs. 
    Anyone who has a copy of that secret key can then verify that that code 
    and message was created by someone with the same key.  
    --  
    **Components:**
      - **Message:** transferring data;
        ```js
        const message = 'my message here';
        ```
      - **Secret key:** private key that contains only sender and receiver;
        ```js
        const secretKey = 'thisIsASecretKey1234';
        ```
      - **Security key:** hashed (secret key + message);
        ```js
        const securityKey = sha256(secretKey + message);
        ```
    **Validation process:**  
    ```js
    // receive securityKey and message
    if (securityKey == sha256(secretKey + message)) {
      // verified!
    }
    ```
    **Examples:**  
      - **MAC (classic scheme):**
        ![link](https://drive.google.com/uc?id=1LWGGMIEoWBItlQrgr1FlsO0hCmoo6Lp-)
      - **MAC for access token** (doesn't have a private key on client, no 
        sense because of XSS):
        ![link](https://drive.google.com/uc?id=1AvASmr3MlcMhf9MI6SZ28H7Mb_IiE3oT)
    
    **Pros:** protect against spoofing and tampering;  
    **Cons:** works bad for microservices arch because each server has to have
    own secret.key and weak to length extension attack (encrypt secret.key by 
    the size of the message).
  - ### HMAC
    **An HMAC** is a kind of MAC. All HMACs are MACs but not all MACs are HMACs.
    The main difference is that an HMAC uses two rounds of hashing instead of
    one (or none). Each round of hashing uses a section of the secret key.
    **Components:**
      - **Message:** transferring data;
        ```js
        const message = 'my message here';
        ```
      - **Secret key:** private key that contains only sender and receiver;
        ```js
        const secretKey = 'thisIsASecretKey1234';
        ```
      - **x2 Hashed Security key:** hashed(secret key + hashed (secret key + message));
        ```js
        const securityKey = sha256(secretKey + sha256(secretKey + message));
        ```
    **Pros:** protect against spoofing, length extension attack and tampering;  
    **Cons:** works bad for microservices arch because each server has to have 
    own secret.key.