# SOP / CORS

## 1) SOP  (same-origin policy)

**SOP** (same-origin policy) определяет как документ или скрипт, загруженный из одного
источника (origin), может взаимодействовать с ресурсом из другого источника. Это помогает
изолировать потенциально вредоносные документы, снижая количество возможных векторов атак.

**An origin** (app's address made by cluster) consists of a URI scheme, domain and port 
number.

![link](https://drive.google.com/uc?id=16jtIFxjzBwgn6_zO1kj1MYTP1MKOW-YY)

When a browser sends an HTTP request from one origin to another, any cookies, including 
authentication session cookies, relevant to the other domain are also sent as part of the
request. This means that the response will be generated within the user's session, and 
include any relevant data that is specific to the user. Without the same-origin policy, 
if you visited a malicious website, it would be able to read your emails from GMail,
private messages from Facebook, etc.

## Reason of usage:
When a browser sends an HTTP request from **<ins>one origin to another, any cookies, including
authentication session cookies, relevant to the other domain are also sent as part of the
request.</ins>** This means that the response will be generated within the user's session, and 
include any relevant data that is specific to the user. Without the same-origin policy, 
if you visited a malicious website, it would be able to read your emails from GMail,
private messages from Facebook, etc (SCRF attack).

## Restrictions:
  - ### iframes
    Внутри `<iframe>` находится по сути отдельное окно с собственными объектами document 
    и window. Когда мы обращаемся к встроенному в ифрейм окну, браузер проверяет, имеет
    ли ифрейм тот же источник. Если это не так, тогда доступ будет запрещён (разрешена
    лишь запись в location, это исключение).  
    __   
    **Мы можем обращаться к ним, используя свойства:**
    - **iframe.contentWindow** ссылка на объект window внутри `<iframe>.`
      ```js
        let iframeWindow = iframe.contentWindow; // OK
        let href = iframe.contentWindow.location.href; // ОШИБКА
        iframe.contentWindow.location = '/'; // OK
      ``` 
    - **iframe.contentDocument** – ссылка на объект document внутри `<iframe>`, короткая 
      запись для iframe.contentWindow.document.
      ```js
        let doc = iframe.contentDocument; // ОШИБКА
      ```

  - ### CSS
    Cross-origin CSS can be embedded using a `<link>` element or an @import in a CSS file. 
    The correct Content-Type header may be required.
  - ### Forms
    Cross-origin URLs can be used as the action attribute value of form elements. A web 
    application can write form data to a cross-origin destination.
  - ### Images
    Embedding cross-origin images is permitted. However, reading cross-origin images 
    (such as loading a cross-origin image into a canvas element using JavaScript) is
    blocked.
  - ### Multimedia
    Cross-origin video and audio can be embedded using `<video>` and `<audio>` elements.
  - ### Scripts
    Cross-origin scripts can be embedded; however, access to certain APIs (such as 
    cross-origin fetch requests) might be blocked.
    
## 2) CORS (Cross-origin resource sharing)
**Cross-origin resource sharing (CORS)** is a browser mechanism which enables controlled 
access to resources located outside of a given domain:
  - **Different domain** (eg. site at example.com calls api.com);
  - **Different sub domain** (eg. site at example.com calls api.example.com)
  - **Different port** (eg. site at example.com calls example.com:3001)
  - **Different protocol** (eg. site at https://example.com calls http://example.com)

It extends and adds flexibility to
the same-origin policy (SOP). However, it also provides potential for cross-domain based
attacks, if a website's CORS policy is poorly configured and implemented.  
--  
**CORS** does not provide protection against cross-site request forgery (CSRF) attacks, 
this is a common misconception.
**CORS** is a controlled relaxation of the same-origin policy, so poorly configured CORS 
may actually increase the possibility of CSRF attacks or exacerbate their impact.  
There are various ways to perform CSRF attacks without using CORS, including simple 
HTML forms and cross-domain resource includes.  
--  
В целях безопасности браузеры ограничивают cross-origin запросы, инициируемые скриптами.
Например, XMLHttpRequest и Fetch API следуют политике одного источника (same-origin
policy). Это значит, что web-приложения, использующие такие API, могут запрашивать 
HTTP-ресурсы только с того домена, с которого были загружены, пока не будут использованы
CORS-заголовки.

## Mechanisms:
### 1) Preflight requests:
**A preflight request** occurs when a browser would normally block the request for violating
the same-origin policy. **<ins>The browser makes a HTTP OPTIONS request to the server from 
another origin asking if the request should be allowed.</ins>** The server can either deny the
request or else allow it with restrictions on the allowed headers and methods.

![link](https://drive.google.com/uc?id=1fsoeH2Yyie0YIkK_T8NL_NuSXbGlD7rE)

**Types of requests by CORS:**
1. **Simple (don't trigger CORS preflight mechanism):**  
   - **Methods:** 
     - GET; 
     - HEAD;
     - POST;
   - **Headers:**
     - Accept;
     - Accept-Language;
     - Content-Language;
     - Content-Type (application/x-www-form-urlencoded, multipart/form-data, text/plain);
2. **Hard (trigger CORS preflight mechanism);**
    - **Methods:**
        - PUT;
        - DELETE;
        - CONNECT;
        - OPTIONS;
        - TRACE;
        - PATCH;
    - **Headers:**
      - Accept
      - Accept-Language
      - Content-Language
      - Content-Type (но учтите дополнительные требования ниже)
      - Last-Event-ID
      - DPR
      - Save-Data
      - Viewport-Width
      - Width
      - Content-Type содержит значение, отличное от следующих (application/x-www-form-urlencoded, multipart/form-data, text/plain);
### 2) CORS HTTP headers:
  - **<ins> Access-Control-Allow-Origin </ins>** - specifies a single origin that should be allowed access:
    - `*`- allow acess to any origins;
    - `["http://..."]` - specify allowed origins;
  - **<ins> Access-Control-Allow-Headers </ins>** -  Lists the non-simple headers that can be 
    included on cross-origin requests to this server:
    - `*` - allow all not simple headers;
    - `["Header-"]` - specify allowed headers;
  - **<ins> Access-Control-Allow-Methods </ins>** - Lists the HTTP methods that are allowed:
    - `*` - allow all not simple methods;
    - `["GET, PUT, PATCH"]` - specify allowed methods;
  - **<ins> Access-Control-Allow-Credentials </ins>** - Indicates whether the browser should include 
    credentials on the request. Credentials in this case means browser cookies, saved
    HTTP Basic/Digest passwords, and TLS client certificates:
    - `true` - allow credentials;
    - `false` - don't allow credentials;
    
    **SameSite cookies - incompatible with CORS.** If a cookie is marked as SameSite then 
    it will not be sent on cross-origin requests regardless of any CORS policy and the
    Access-Control-Allow-Credentials header will be ignored. An exception is made for
    origins that are sub-domains of the same site, for example www.example.com can 
    still send requests to api.example.com, but genuine cross-site requests are 
    disallowed. If you need to allow cross-site requests with cookies, then you should
    not use SameSite cookies.
  - **<ins> Access-Control-Max-Age </ins>** - Indicates the maximum number of seconds that the browser 
    should cache this CORS response. Browsers typically impose a hard-148 coded upper 
    limit on this value of around 24 hours or less (Chrome currently limits this to 
    just 10 minutes). This only applies to the allowed headers and allowed methods.
  - **<ins> Access-Control-Expose-Headers </ins>** - Only a small set of basic headers are exposed from
    the response to a cross-origin request by default. Use this header to expose any 
    non- standard headers that your API returns in responses.