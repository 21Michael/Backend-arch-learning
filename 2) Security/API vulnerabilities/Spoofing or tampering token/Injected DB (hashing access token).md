# Injected DB (hashing access token)

## Preventing mechanisms:
  - **Preventing DB injections** (https://github.com/21Michael/Backend-arch-learning/tree/main/2)%20Security/API%20vulnerabilities/Injections/DB);
  - **Hashing the access token before saving to DB**  
    If an attacker has access to DB he can gain access to every user's 
    access token, for preventing this we should make an access token, send it 
    to the client, hash it before saving to DB and every authentication we're
    getting token from client, hashing it ang compare hashed tokens;  
    **Pros:** even in a hacker has access to DB he doesn't know users token;  
    **Cons:** hacker has an ability to exchange users token to own and get an 
    access + XSS + intercepting;