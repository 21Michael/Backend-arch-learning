# Access control techniques:
**Authentication** confirms that users are who they say they are.  
**Authorization** gives those users permission to access a resource.

![link](https://res.cloudinary.com/practicaldev/image/fetch/s--VYXihGsl--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/ras8no1uj4ih1ogzy89h.png)

## Authentication
Authentication is the act of validating that users are whom they claim to be. This 
is the first step in any security process.

**Complete an authentication process with:**
  - **Passwords.** Usernames and passwords are the most common authentication factors. If a user enters the correct data, the system assumes the identity is valid and grants access.
  - **One-time pins.** Grant access for only one session or transaction.
  - **Authentication apps.** Generate security codes via an outside party that grants access.
  - **Biometrics.** A user presents a fingerprint or eye scan to gain access to the system.

## Authorization
Authorization in system security is the process of giving the user permission to access 
a specific resource or function. This term is often used interchangeably with access 
control or client privilege.

Giving someone permission to download a particular file on a server or providing
individual users with administrative access to an application are good examples of
authorization.

In secure environments, authorization must always follow authentication. Users should 
first prove that their identities are genuine before an organization’s administrators 
grant them access to the requested resources.

![link](https://www.outsystems.com/blog/-/media/images/blog/posts/authentication-vs-authorization/table-bp-authentication-vs-authorization.png?updated=20211102150423)