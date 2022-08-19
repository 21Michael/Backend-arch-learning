# Delegated authorization (OAuth 2.0)

**<ins>OAuth</ins>** -  is an open-standard authorization protocol or framework that describes how 
unrelated servers and services can safely allow authenticated access to their assets 
without actually sharing the initial, related, single logon credential. In authentication 
parlance, this is known as secure, third-party, user-agent, delegated authorization. 

**<ins>OAuth 2.0</ins>** is designed only for authorization to 3-th party services (your API 
auth, Google, Facebook, LinkedIn... auth) with established actions that user can perform, for 
granting access to data and features from one application to another. 

## Client Types Authorization:
  - ### Confidential client: Web Application (client-secret-key auth)
    A web application is an application running on a web server. In reality, a web 
    application typically consists of both a browser part and a server part. If a 
    web application needs access to a resource server (e.g. to Facebook user accounts),
    then the client password could be stored on the server. The password would thus 
    be confidential.   
    ![link](http://tutorials.jenkov.com/images/oauth2/overview-client-types-1.png)
    
    **Authorization by <ins>client-secret-key</ins> throughout the <ins>back channel</ins>:**  
    ![link](https://drive.google.com/uc?id=1Af7YY0gx1PlMPccuChoq561xA17uhGFT)
    
  - ### Public client: User Agent Application (PKCE auth)
    A user agent application is for instance a JavaScript application running in a 
    browser. The browser is the user agent. A user agent application may be stored 
    on a web server, but the application is only running in the user agent once
    downloaded. An example could be a little JavaScript game that only runs in the
    browser.   
    ![link](http://tutorials.jenkov.com/images/oauth2/overview-client-types-2.png)
    
  - ### Public client: Native Application (PKCE auth)
    A native application is for instance a desktop application or a mobile phone 
    application. Native applications are typically installed on the users computer
    or device (phone, tablet etc.). Thus, the client password will be stored on the
    users computer or device too.  
    ![link](http://tutorials.jenkov.com/images/oauth2/overview-client-types-3.png)
    
    **Authorization without <ins>PKCE</ins> throughout the <ins>front channel</ins>:**  
    ![link](https://drive.google.com/uc?id=1bUEfTM5HjQPGRNTCVutTYv7QRZULvvZc)
   
    **Authorization by <ins>PKCE</ins> throughout the <ins>front channel</ins>:**
    ### PKCE
    **PKCE** is an extension to the Authorization Code flow to prevent 
    CSRF and authorization code injection attacks. PKCE is not a replacement for a 
    client secret, and PKCE is recommended even if a client is using a client secret.
    PKCE was originally designed to protect the authorization code flow in mobile 
    apps, but its ability to prevent authorization code injection makes it useful for
    every type of OAuth client, even web apps that use a client secret.
    ![link](https://drive.google.com/uc?id=1fD9lCI9xOd5WZsKw62gUyCOe9_NKYhsZ)
    
## Data transferring channels:
![link](https://drive.google.com/uc?id=15NSAUUxP3FQd6zoDMRyGAO6XiO1zb2M3)
