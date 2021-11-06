# Backend-arch-learning
Learning backend architecture, security, optimization, NodeJS... 

## 1) Computer Networks:
  - **Networks;**  ✅
  - **Protocols stack:**
    - **ISO (layers):**
      - `1. Application:`
          - HTTP:
            1. Messages; ✅
            2. Cache; ✅
            3. Methods; ✅
            4. Response codes; ✅
            5. HTTP 1.0 vs HTTP 2.0; ✅
            6. CORS;
          - Telnet; ✅
          - FTP; ✅
          - SMTP; ✅
          - DNS; ✅
          - NFS; ✅
          - SSH; ✅
          - WebSocket;
          - ...
      - `2. Presentation:` ✅
          - ASCII; ✅
          - MIDI; ✅
          - SSL; ✅
          - JPEG
          - ...
      - `3. Session:` ✅
          - PPTP; ✅
          - L2TP; ✅
          - ...
      - `4. Transport:` ✅
          - TCP; ✅
          - UDP; ✅
          - ...
      - `5. Network:` ✅
          - IP; ✅
          - ICMP; ✅
          - ARP; ✅
          - ...
      - `6. Data link:`  ✅
          - MAC (sublevel);  ✅
          - LLC (sublevel);  ✅
          - Ethernet;  ✅
          - PPP;  ✅
          - DSL;  ✅
          - ...
      - `7. Physical:` ✅
    - **TCP/IP (layers):**  
      - `1. Application:`
      - `2. Transport:`
      - `3. Internet:`
      - `4. Network Interface:`
  - **Cookie / Session / LocalStorage;**
  - **VPN;**

## 2) Security:
  - **API security:**
    - **Information security:**
      - <ins>Access control techniques:</ins>
        - Authentication:
          - SSO; -------------------------------
        - Authorization:
          - Basic auth; -------------------------------
          - Bearer token; -------------------------------
          - JWT;  -------------------------------
          - OAuth;  -------------------------------
          - PKCE; -------------------------------
      - <ins>Backup and recovery optimization;
      - <ins>Data masking;
      - <ins>Cryptography:</ins>
        - Symmetric Encryption Methods; -------------------------------
        - Asymmetric Encryption Methods;  -------------------------------
        - Hashing Methods;  -------------------------------
      - ...
    - **Network security:**
      -  <ins>Firewalls; 
      -  <ins>Load-balancers;
      -  <ins>Reverse proxies;
      -  <ins>SOP/CORS;</ins> -------------------------------
      -  <ins>SSL/HTTPS;</ins> -------------------------------
      -  <ins>Designing ACL;</ins> -------------------------------
      -  ...
    - **Application security:**
      -  <ins>Coding techniques;
      -  <ins>Software security vulnerabilities
      -  <ins>Store and manage system and user credentials used to access your API;
      -  ...
  - **Security aspect of designing API:**
    - **Assets;**
    - **Mechanisms:**
      - <ins>Rate-limit;
      - <ins>Authentication;
      - <ins>Audit-logging;
      - <ins>Access control (authorization);
    - **Processing Environment;**
  - **API vulnerabilities:**
    - **OWASP**;  -------------------------------
    - **Injections:**
      - <ins>SQL / NoSQL Injections;</ins> -------------------------------
      - <ins>XSS;</ins> -------------------------------
    - **CSRF;** -------------------------------
    - **DDoS;** -------------------------------
  
## 3) Architecture:
**Link:** https://ru.wikipedia.org/wiki/%D0%A8%D0%B0%D0%B1%D0%BB%D0%BE%D0%BD_%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F

### 3.1) API architectural styles (server - client):
  - **REST:**
    - <ins>JSONApi spec;
    - <ins>REST-full Principles:</ins>
    - <ins>Swagger;</ins>
    - <ins>HATEOAS;</ins>
  - **RPC:** ✅
    - <ins>XHL-RPC; ✅
    - <ins>JSON-RPC; ✅
    - <ins>gRPC; ✅
  - **GraphQL:**
 
### 3.2) Code organization:
  - **Code separation;**
  - **File naming;**
  - **Modules:**
    - Circular dependencies;
### 3.3) System Architectural patterns:
  - **Model-View-Controller (MVC);**
  - **Model-View-Presenter;**
  - **Model-View-ViewModel;**
  - **Presentation-Abstraction-Control;**
  - **Naked objects;**
  - **Hierarchical Model-View-Controller;**
  - **View-Interactor-Presenter-Entity-Routing (VIPER);**
### 3.4) Software Architectural pattern:
  - **Event-driven architecture;**
  - **Layered architecture;**
  - **Hexagonal architecture;**
  - **Microservices architecture;**
  - **Monolith architecture;**
### 3.5) Other:
  - **Heartbeat/Health check;**
  - **SaaS;**
  - **FaaS;**
  - **Long-Pooling;**

## 4) NodeJS:
  - **Express;**
  - **Streams;**
  - **Require process;**
  - **Event Loop;**
  - **Events:**
    - **Event-driven development;**
    - **Understanding of node's event system;**
    - **Ability to write custom events.**

## 5) Database:
**Link:** https://github.com/21Michael/SQL-Study-Project

## 6) AWS

- ETL
- SSR