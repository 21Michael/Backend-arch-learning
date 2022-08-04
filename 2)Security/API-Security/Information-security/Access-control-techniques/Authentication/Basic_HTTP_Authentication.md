# Basic HTTP Authentication
Using basic HTTP authentication by putting username and password that were encoded 
(using the Base64 encoding) in special Authorization header.

![link](https://drive.google.com/uc?id=1aLo6sd1zk9StE-KAG-qAh1RpIL95G1lY)

## Security vulnerability:
  - The user’s password is sent on every API call, increasing the chance of it 
    accidentally being **<ins>exposed by a bug</ins>** in one of those operations. If you are 
    implementing a microservice architecture, then every microservice needs to 
    securely handle passwords.
  - **<ins>Verifying a password is an expensive operation,</ins>** as you saw in chapter 3, and 
    performing this validation on every API call adds a lot of overhead. Modern
    password-hashing algorithms are designed to take around 100ms for interactive 
    logins, which limits your API to handling 10 operations per CPU core per second.
    You’re going to need a lot of CPU cores if you need to scale up with this design!
  - The dialog box presented by browsers for HTTP Basic authentication is pretty ugly,
    with **<ins>not much scope for customization.**</ins> The user experience leaves a lot to be desired.
  - There is **<ins>no obvious way for the user to ask the browser to forget the password.**</ins>  
    Even closing the browser window may not work and it often requires configuring 
    advanced settings or completely restarting the browser. On a public terminal, 
    this is a serious security problem if the next user can visit pages using your 
    stored password just by clicking the back button.

## Conclusion:
  - Very unsafe;
  - Difficult for implementation for micro-services;
  - Slow;
  - Advance settings;
  - No customization;