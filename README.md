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
  - **REST:** ✅
    - <ins>REST-full Principles:</ins> ✅
    - <ins>HATEOAS;</ins> ✅
  - **RPC:** ✅
    - <ins>XHL-RPC;</ins> ✅
    - <ins>JSON-RPC;</ins> ✅
    - <ins>gRPC;</ins> ✅
  - **GraphQL;** ✅
  - **SOAP;**

### 3.2) Client-Server communication specification:
  - **JSONApi spec;**

### 3.3) Code organization:
  - **Code separation;**
  - **File naming;**
  - **Modules:**
    - Circular dependencies;
  
### 3.4) System Architectural patterns:
  - **Model-View-Controller (MVC);**
    - **Model-View-Presenter;**
    - **Model-View-ViewModel;**
  - **Presentation-Abstraction-Control;**
  - **Naked objects;**
  - **Hierarchical Model-View-Controller;**
  - **View-Interactor-Presenter-Entity-Routing (VIPER);**

### 3.5) Software Architectural patterns:
  - ### Monolithic architecture:
    - **Layered (n-tier) architecture pattern:** ✅
    - **Microkernel (plug-in) Architecture pattern;** ✅
    - **Pipe-Filter Architecture pattern;**
  - ### Distributed architecture:
    - **Event-driven architecture pattern;** ✅
    - **Microservices architecture pattern:**  ✅
      - Conceptions and principles:  ✅
        - DB management (DB per service); ✅
        - Communication principle: ✅
          - Sync communication (inter-service communication); ✅
          - Async communication (Event Bus); ✅
        - Independent principle; ✅
        - Event synchronization; ✅
      - Deployment Tools:  ✅
        - Docker; ✅
        - Kubernetes; ✅
        - Skaffold; ✅
      - Deployment Flow:  ✅
        - SSR vs CSR; ✅
        - Share common logic between services: ✅
          - Repeat files in each service; ✅
          - Common repository;  ✅
          - NPM registry; ✅
        - Work flow: ✅
          - Repository types: ✅
            - Monorepository; ✅
            - Repository per service; ✅
          - Deployment flow; ✅
      - Security:  ✅
        - Authorization services concepts; ✅
        - JWT Auth; ✅
        - Session ID Auth; ✅
    - **Space-Based Architecture pattern;**
    - **Service-oriented architecture pattern;**
  - ### Hexagonal architecture pattern;
  - ### Client-Server Architecture pattern;
  - ### Master-Slave Architecture pattern;
  - ### Serverless architecture pattern;
### 3.6) Other:
  - **Heartbeat/Health check;**
  - **SaaS;**
  - **FaaS;**
  - **Long-Pooling;**
  - **Swagger;**

## 4) NodeJS:
  - **Frameworks:**
    - **Express:**
      - routing;
      - middleware;
  - **Engine mechanisms:**
    - **Garbage collector;**
    - **Streams;**
    - **Asynchronicity / Event Loop;**
    - **Node's event system;**
  - **Embedded functionality:**
    - **RELP;**
    - **Streams API;**
    - **Events:**
      - **Event-driven development;**
      - **Ability to write custom events;**
    - **Require Process;**

## 5) Database:
**Link:** https://github.com/21Michael/SQL-Study-Project

## 6) AWS

- ETL
- SSR