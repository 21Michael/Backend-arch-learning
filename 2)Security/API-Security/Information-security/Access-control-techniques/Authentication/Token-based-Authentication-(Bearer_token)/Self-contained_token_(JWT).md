# Self-contained token (JWT)

## JOSE
**JOSE** - The standard provides a general approach to signing and encryption of any
content, not necessarily in JSON. However, it is deliberately built on JSON and 
base64url to be easily usable in web applications. Also, while being used in 
OpenID Connect, it can be used as a building block in other protocols (JWT, JWE,
JWA, JWS, JWK).

![link](https://image.slidesharecdn.com/20180220webhack11overviewofjsonobjectsigningandencryption-180226064217/95/overview-of-json-object-signing-and-encryption-7-638.jpg?cb=1519627630)

## JOSE protocols:

## JWT
**JWT** - это открытый стандарт (RFC 7519) для создания токенов доступа, 
основанный на формате JSON. Authorization / Authentication mechanism that
crypts any data we want (usually user data) on server, sends back to browser 
and lately uses for Authorization by decrypting it. Has to be managed manually. 
Could be transported into http header, body or cookie. Supports by diff 
programs platforms (Java, Ruby, JS...).

### JWT specification formats:
  - ### JWS
    **JWS (JSON WEB SIGNATURE):** represents content secured with digital signatures
    or Message Authentication Codes (MACs) using JSON-based data structures;
    ![link](https://miro.medium.com/max/875/1*sz6bIndG2bTBGcZ8ocmM5Q.png)
    
  - ### JWE
    **JWE (JSON WEB ENCRYPTION):** is an IETF standard providing a standardised 
    syntax for the exchange of encrypted data, based on JSON and Base64. It is
    defined by RFC7516.
    ![link](https://miro.medium.com/max/875/1*-qEUNh7EYxBbnnt0Xk997g.png)
    
### Scheme (JWT as JWS):
![link](https://drive.google.com/uc?id=14bKoarW-yLGHVwWSvDc0nRnYI5wMqCJK)

## JWA
**JWA (JSON WEB ALGORITMS):** specification registers cryptographic algorithms and
identifiers to be used with the JSON Web Signature (JWS), JSON Web Encryption (JWE),
and JSON Web Key (JWK) specifications.

**JWA signature mechanisms:**
  - **Asymmetric:** RSA or ECDSA... (relevant for sub-domain authentication);
  - **Symmetric:** AES, DES... (relevant for one domain apps);
  - **HASH functions:** SHA256...;

![link](https://hacksandsecurity.org/sites/default/files/u3/1_23RpkZuWAeSP7x0YdMtsdQ.png)

**JWA encrypting algorithms:**
![link](https://www.cryptomathic.com/hubfs/Images_misc/Blog-Photos/Table-Algorithms-Key-Management.png)

![link](https://www.researchgate.net/profile/Juan-Burguillo/publication/260402686/figure/tbl2/AS:669102762901509@1536537938575/List-of-supported-encryption-algorithms-and-its-main-features.png)

## JWK
**JWK (JSON WEB KEY):** is a JavaScript Object Notation (JSON) data structure that
represents a cryptographic key.