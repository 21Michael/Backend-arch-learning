# Brute force attack
A brute force attack is a trial-and-error method used to decode sensitive data. The most
common applications for brute force attacks are **cracking passwords and cracking encryption
keys (keep reading to learn more about encryption keys).** Other common targets for brute 
force attacks are **API keys and SSH logins.** Brute force password attacks are often carried
out by scripts or bots that target a website's login page.

![link](https://www.cloudflare.com/img/learning/security/threats/brute-force-attack/brute-force-cracking-time.png)

## Preventing mechanisms:
Users of web services can decrease their vulnerability to brute force attacks:
  - By choosing longer, more complex passwords;
  - Encryption method: A longer encryption key is exponentially more secure than a 
    shorter one. For example, in a `128-bit` encryption key, there are 2128 possible
    combinations a brute force attacker would have to try. For `256-bit` encryption,
    an attacker would have to try 2256 different combinations, which would require
    2128 times more computational power to crack than a 128-bit key!
    (2128 = 340,282,366,920,938,463,463,374,607,431,768,211,456 possible combinations).
  - It is also recommended enabling two-factor authentication;
  - Use unique passwords for each service. If an attacker is able to brute force a 
    user’s password for one service, that attacker may try recycling the same login 
    and password on many other popular services. This is known as **credential stuffing.**