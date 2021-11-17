# Session fixation

**Session fixation** - is an attack that permits an attacker to hijack a valid 
user session. Hacker replaces session token on his own for victim's session before
he made his own session token. 

**<ins>Most common stealing techniques:</ins>**
  - **<ins>Session token in the URL argument:</ins>** The Session ID is sent to the victim in a
    hyperlink and the victim accesses the site through the malicious URL.
  - **<ins>Session token in a hidden form field:</ins>** In this method, the victim must be 
    tricked to authenticate in the target Web Server, using a login form 
    developed for the attacker. The form could be hosted in the evil web server
    or directly in html formatted e-mail.
  - **<ins>Session ID in a cookie:</ins>** Most browsers support the execution of client-side 
    scripting. In this case, the aggressor could use attacks of code injection 
    as the XSS (Cross-site scripting) attack to insert a malicious code in the
    hyperlink sent to the victim and fix a Session ID in its cookie.
    
![link](https://www.checkmarx.com/wp-content/uploads/2016/02/SF.jpg)

## Preventing mechanisms:
  - **Don't save it in URL** (very easy to steal);
  - **Before authorization clean session token** if it already axists and make
    a new token by decrypting current users' id;
  - If token saved in cookie use **Cookie security attributes;**
    ### Cookie security attributes:
    - **<ins>HttpOnly:</ins>** the “HttpOnly” flag blocks the access of the 
      related cookie from the client-side (it can’t be used from Javascript 
      code): if an attacker was to succeed in injecting some javascript (XSS)
      despite all your precautions, he won’t be able to access the cookies 
      anyway. That will significantly limit the attack range.
    - **<ins>Secure flag:</ins>** forbid to use a cookie without HTTPs.
    - **<ins>SameSite:</ins>** SameSite cookies will only be sent on requests 
      that originate from the same origin as the cookie (*even if CORS allows 
      to send credentials to cross-domain requests, see SOP/CORS chapter).
    - **<ins>Domain:</ins>** If no Domain attribute is present, then a cookie 
      will only be sent on requests to the exact host that issued the Set-Cookie
      header. This is known as a host-only cookie.
    If you set a Domain attribute, then the cookie will be sent on requests to
      that domain and all sub-domains. For example, a cookie with 
      Domain=example.com will be sent on requests to api.example.com and 
      www.example.com.
    - **<ins>Path:</ins>** If the Path attribute is set to /users, then the 
      cookie will be sent on any request to a URL that matches /users or any
      sub-path such as /users/mary, but not on a request to /cats/mrmistoffelees.
      The Path defaults to the parent of the request that returned the 
      Set-Cookie header, so you should normally explicitly set it to / if you
      want the cookie to be sent on all requests to your API. The Path attribute
      has limited security benefits, as it is easy to defeat by creating a 
      hidden iframe with the correct path and reading the cookie through the DOM.
    - **<ins>Expires and Max-Age:</ins>** Sets the time at which the cookie 
      expires and should be forgotten by the client, either as an explicit date 
      and time (Expires) or as the number of seconds from now (Max-Age). 
      Max-Age is newer and preferred, but Internet Explorer only understands
      Expires. Setting the expiry to a time in the past will delete the cookie
      immediately. If you do not set an explicit expiry time or max-age, then
      the cookie will live until the browser is closed.
  - **Validating a session cookie** token expiration, request attributes...;