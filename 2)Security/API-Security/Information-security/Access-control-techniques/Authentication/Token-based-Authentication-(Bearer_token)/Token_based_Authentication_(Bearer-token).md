# Token based Authentication

**<ins>TOKEN BASED AUTHENTICATION</ins>** - rather than send the username and password directly to
the API endpoint (HTTP basic auth), the client instead sends them to a dedicated login
endpoint. The login endpoint verifies the username and password and then respond with 
a time-limited token. The client then includes that token on subsequent API requests
to authenticate. The API endpoint can authenticate the token because it is able to 
talk to a token store that is shared between the login endpoint and the API endpoint.

**<ins>Token authentication types:</ins>**  
- **Access token:**   
  Is a token that you will have to add in all 
  request headers to be authenticated as a concrete user. Create certain token to the
  certain user. That require saving the token in DB;
- **Bearer (владелец) token:**   
  Is a token that can be used at an API simply
  by including it in the request. Bearer can be simply understood as `"give access to 
  the bearer of this token"`. Self-contained and doesn't require saving to the DB.
  One valid token and no question asked. Any client that has a valid token is authorized 
  to use that token and does not need to supply any further proof of authentication. 
  A bearer token can be given to a third party to grant them access without revealing 
  user credentials but can also be used easily by attackers if stolen;

## Security vulnerabilities:
  - **Session token fixation:** session-id tokens;
  - **Cross-site request forgery (CSRF):** tokens that saved in cookies; 
  - **Stealing or decrypting by XSS:** for all kinds of tokens an attacker has access
    to real users' data on client/server side by XSS.
  - **Spoofing or tampering token by injected DB:** an attacker doesn't have access to real users' data,
    but he can replace decrypted users data for his own decrypted data;
