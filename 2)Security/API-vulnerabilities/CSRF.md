# CSRF (only for tokens that stored inside of cookie)
Is an attack that forces an end user to execute unwanted actions on a web application in
which they’re currently authenticated. With a little help of social engineering (such as
sending a link via email or chat), an attacker may trick the users of a web application
into executing actions of the attacker’s choosing. **This attack based on the fact that 
browser sent same cookie that used in current session to every request from current site
(to attakers link).**

## Scheme:
![link](https://drive.google.com/uc?id=1TqeLu-KsfHGU0w_p4tOj1vPjdravbzCp)

## HTTP requests that should be protected:
Если вы пишете свой Web-Сервис в соотвествии со стандартом RFC7231, то методы GET, 
HEAD, OPTIONS и TRACE являются безопасными: они предназначены только для получения 
информации и не должны изменять состояние сервера.

Таким образом, защищать необходимо небезопасные методы, к которым относятся: **POST, 
PUT, DELETE, PATCH.**

## Preventing mechanisms:

### 1) HTTP Cookie security attributes (not always possible):
  - **SameSite attribute:**  
    - **SameSite=strict** - cookies will not be sent on any cross-site request including
      when a user just clicks on a link from one site to another. This can be quite 
      surprising behavior that can break traditional websites (works fine for SPA);
    - **SameSite=lax** - allows cookies to be sent when a user directly clicks on a link 
      but will still block cookies on most other cross-site requests.
      
  ![link](https://maxlead.com/wp-content/uploads/2020/02/labeling-2-en.png)

  <ins>**The problem:**</ins>
  - SameSite cookies are a good additional protection measure against 
    CSRF attacks, but **they are not yet implemented by all browsers and frameworks.**
  - Because the notion of same site includes sub-domains, they also provide little 
    protection against **<ins>sub-domain hijacking attacks.</ins> The protection against 
    CSRF is as strong as the weakest sub-domain of your site: if even a single sub-domain
    is compromised, then all protection lost.**
  - **SameSite cookies - incompatible with CORS.** If a cookie is marked as SameSite then 
    it will not be sent on cross-origin requests regardless of any CORS policy and the
    Access-Control-Allow-Credentials header will be ignored. An exception is made for 
    origins that are sub-domains of the same site, for example www.example.com can still
    send requests to api.example.com, but genuine cross-site requests are disallowed. **If 
    you need to allow cross-site requests with cookies, then you should not use SameSite 
    cookies.**

### 2) Hash-based double-submit cookies (CSRF token) (the best way):
Эффективным и общепринятым на сегодня способом защиты от CSRF-Атаки является токен. 
Под токеном имеется в виду случайный набор байт, который сервер передает клиенту, 
а клиент возвращает серверу.

Защита сводится к проверке токена, который сгенерировал сервер, и токена, который
прислал пользователь.

**Implementations:**
  1) **<ins>Synchronizer Tokens (Statefull: saved in session storage on server) in hidden input field:**</ins>  
     The best pattern for preventing CSRF in traditional web applications is to 
     generate a random string and store it as an attribute on the session. **Whenever
     the application generates an HTML form, it includes the random token as a hidden 
     field. When the form is submitted, the server checks that the form data contains
     this hidden field and that the value matches the value stored in the session 
     associated with the cookie.** Any form data that is received without the hidden 
     field is rejected.
     ```html
      <input type="hidden" name="csrf-token" value="CIwNZNlR4XbisJF39I8yWnWX9wX4WFoz" />
     ```
     Hidden inputs are completely invisible in the rendered page, and there is no way 
     to make it visible in the page's content.
     
     **<ins>The problem:**</ins> an **API does not allow adding hidden form fields to 
     requests** because most API clients want JSON or another data format rather than HTML.
  
  2) **<ins>Synchronizer Tokens (Statefull: saved in session storage on server) in X-CSRF-Token header:**</ins>   
     An alternative is to require that calls to your API **include a random token in a 
     custom header, such as X-CSRF-Token,** along with the session cookie. A common
     approach is to store this extra random token as a second cookie in the browser
     and require that it is sent as both a cookie and an X-CSRF-Token header on each
     request. This second cookie is not marked HttpOnly, so that it can be read from 
     JavaScript (but only from the same origin).
     ![link](https://a.kabachnik.info/assets/drgalleries/images/blog/sap/xsrf/thumb3_718x307_sap_xsrf_workflow.png)

     **<ins>The problem:**</ins> This traditional solution has some problems, because 
     while it is not possible to read the valueof the second cookie (X-CSRF-Token in
     header) from another origin, there are a number of ways that the cookie could be
     overwritten by the attacker with a known value, which would then let them forge 
     requests.(make own X-CSRF-Token header and put valid token that was stolen by XSS...).
     
  3) **<ins>Double Submit Cookie + Encrypted Token (Stateless):**</ins>  
     Rather than generating a second random cookie, you will run the original session
     cookie through a cryptographically secure hash function to generate the second
     token. This ensures that any attempt to change either the anti-CSRF token or the
     session cookie will be detected because the hash of the session cookie will no 
     longer match the token. As the attacker cannot read the session cookie, they are
     unable to compute the correct hash value.
     ![link](https://drive.google.com/uc?id=1RgcK-lVTiL5oiFuiKeFfK8qciDbNxUOv)

     **<ins>Take care:**</ins> The security of this scheme depends on the security of the hash function. If the attacker can
     easily guess the output of the hash function without knowing the input, then they can guess the
     value of the CSRF cookie. For example, if the hash function only produced a 1-byte output, then
     the attacker could just try each of the 256 possible values.
     