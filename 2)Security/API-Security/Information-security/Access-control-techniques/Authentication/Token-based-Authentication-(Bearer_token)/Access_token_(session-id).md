# Access token (session-id)

**<ins>Session ID</ins>** - is a unique number that a Web site's server assigns a specific user for
the duration of that user's visit (session). The session ID can be stored as a cookie,
form field, or URL. By itself there is no user information.  When server receives a 
SessionID, it needs to do extra work to find out which user it belongs to, and then 
what s/he can do. This extra work often requires a database lookup.

**<ins>Stored by:**</ins>
  - **<ins>Cookie (most common used)</ins>** - transport mechanism that transports small piece 
    of data that a server sends to the user's web browser. The browser may store it 
    and send it back with later requests to the same server.                 
    __  
    **<ins>Pros:**</ins> managed automatically by browser, easy to Implement, has many customizations,
    fast.  
    **<ins>Const:**</ins> exposed to CSRF attacks, SameSite protection incompatible 
    with CORS, browsers not always allow using cookies.
    

  - **<ins>Local-storage/session-storage</ins>** - after user logged in create a session token, saved it inside
    DB and sent it to user inside Authorization header, save it on client side 
    (local-storage/session-storage (auth token has to be created for each new 
    tabs)/indexedDB) and add it to each request.  
    __   
    **<ins>Pros:**</ins> doesn't have vulnerabilities related to cookie;  
    **<ins>Const:**</ins> XSS attacks for client side, SQL injections for server side, expensive 
    calculations (every request extracts token and user from DB);
    
![link](https://drive.google.com/uc?id=1_Pp7v_JIIenX66FUR1zOXac3HN_ue4bA)
