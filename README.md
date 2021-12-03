# Backend-arch-learning
Learning backend architecture, security, optimization, NodeJS... 

## 1) Computer Networks:
  - **Networks;**  ✅
  - **Protocols stack:**
    - **OSI (layers):**
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
          - WebSocket;
          - ...
      - `2. Presentation:` ✅
          - ASCII; ✅
          - MIDI; ✅
          - SSH; ✅
          - SSL / TLS; ✅
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
        - Authentication/Authorization token storage/transport; ✅
        - Authentication:
          - Basic HTTP Authentication; ✅
          - Token based Authentication (Bearer token):
            - Access token (session-id); ✅
            - Self-contained token (JWT / JOSE);  ✅
          - Open ID Connect Authentication (OAuth 2.0); ✅
        - Authorization:
          - SSO; ✅
          - Delegated authorization (OAuth 2.0) + PKCE;  ✅
      - <ins>Backup and recovery optimization;
      - <ins>Data masking;
      - <ins>Cryptography:</ins>
        - Symmetric Encryption Methods; ✅
        - Asymmetric Encryption Methods; ✅
        - Hashing Functions; ✅
      - ...
    - **Network security:**
      -  <ins>Firewalls; 
      -  <ins>Load-balancers;
      -  <ins>Reverse proxies;
      -  <ins>SOP / CORS;</ins> ✅
      -  <ins>Designing ACL;</ins>
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
    - **OWASP**; ✅
    - **Injections:**
      - **DB:**
        - <ins>SQL;</ins> ✅
        - <ins>NoSQL Injections;</ins> ✅
      - **JS:**     
        - <ins>XSS;</ins> ✅
    - **Spoofing or tampering token:** 
      - **Session token fixation;** ✅
      - **Injected DB (hashing access token);** ✅
      - **Injected client + interception (MAC / HMAC signature);** ✅
    - **CSRF;** ✅
    - **DDoS;** ✅
    - **Brute force attack;** ✅
  
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
  - ### Serverless architecture pattern:
    - **SaaS;**
    - **FaaS;**
### 3.6) Other:
  - **Heartbeat/Health check;**
  - **Long-Pooling;**
  - **Swagger;**

## 4) NodeJS:
  - **Frameworks:**
    - **Express:**
      - routing;
      - middleware;
  - **Engine mechanisms:**
    - **NodeJS:**
      - **Engine V8:** ✅
        - **Execution context:**
          - Global execution context; ✅
          - Functional execution context; ✅
          - Lexical environment; ✅
        - **Execution Stack + Heap;** ✅
          - JS memory model; ✅
        - **Execution process (https://github.com/21Michael/JS-arch-learning/blob/main/JavaScript/6)%20Optimization%20techniques/Language-specific%20optimizations/JIT/JIT.md):** ✅
          - Parser; ✅
          - Interpreter; ✅
          - JIT Compiler; ✅
        - **Garbage collector;** ✅
      - **libuv:**
        - Asynchronicity / Event Loop;
        - Thread pool;
      - **Execution flow;** ✅
    - **Streams;**
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