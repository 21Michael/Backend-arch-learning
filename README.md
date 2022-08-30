# Backend-arch-learning
Learning backend architecture, security, optimization, NodeJS... 

## 1) Computer Networks:
  - [**Networks**](1\)Computer-Networks/Networks/Comp_Networks.md)  
  - **Protocols stack:**
    - **OSI (layers):**
      1. **Application:**
          - [HTTP](1\)Computer-Networks/Protocols-stack/OSI/1.Application/HTTP.md):
            1. Messages; ✅
            2. Cache; ✅
            3. Methods; ✅
            4. Response codes; ✅
            5. HTTP 1.0 vs HTTP 2.0; ✅
          - [Telnet](1\)Computer-Networks/Protocols-stack/OSI/1.Application/Application.md); 
          - [FTP](1\)Computer-Networks/Protocols-stack/OSI/1.Application/Application.md); 
          - [SMTP](1\)Computer-Networks/Protocols-stack/OSI/1.Application/Application.md); 
          - [DNS](1\)Computer-Networks/Protocols-stack/OSI/1.Application/Application.md); 
          - [NFS](1\)Computer-Networks/Protocols-stack/OSI/1.Application/Application.md); 
          - WebSocket;
          - ...
      2. [**Presentation:**](1\)Computer-Networks/Protocols-stack/OSI/2.Presentation/Presentation.md)
          - ASCII; ✅
          - MIDI; ✅
          - [SSH](1\)Computer-Networks/Protocols-stack/OSI/2.Presentation/SSH.md); ✅
          - [SSL/TLS](1\)Computer-Networks/Protocols-stack/OSI/2.Presentation/SSL_TLS.md); ✅
          - JPEG
          - ...
      3. [**Session:**](1\)Computer-Networks/Protocols-stack/OSI/3.Session/Session.md)
          - PPTP; ✅
          - L2TP; ✅
          - ...
      4. [**Transport:**](1\)Computer-Networks/Protocols-stack/OSI/4.Transport/Transport.md);
          - TCP; ✅
          - UDP; ✅
          - ...
      5. [**Network:**](1\)Computer-Networks/Protocols-stack/OSI/5.Network/Network.md)
          - IP; ✅
          - ICMP; ✅
          - ARP; ✅
          - ...
      6. [**Data link:**](1\)Computer-Networks/Protocols-stack/OSI/6.Data-Link/Data_Link.md)
          - MAC (sublevel);  ✅
          - LLC (sublevel);  ✅
          - Ethernet;  ✅
          - PPP;  ✅
          - DSL;  ✅
          - ...
      7. **[Physical](1\)Computer-Networks/Protocols-stack/OSI/7.Physical/Physical.md):** ✅
    - **TCP/IP (layers):**  
      - `1. Application:`
      - `2. Transport:`
      - `3. Internet:`
      - `4. Network Interface:`
  - **Cookie / Session / LocalStorage;**
  - **VPN;**
  - **Communication paradigms:**
    - [Messages:](1\)Computer-Networks/Communication-paradigms/Messages.md) 
      - Types; ✅
      - Exchange types; ✅
    - [Request-Response:](1\)Computer-Networks/Communication-paradigms/Request_Response.md) 
      - Sync / async; ✅
    - [One-way notifications](1\)Computer-Networks/Communication-paradigms/One-way_notifications.md)  
    - [Publisher-Subscriber](1\)Computer-Networks/Communication-paradigms/Publisher_Subscriber.md) 
    - [Publish / Async-Response (publish/subscribe + request/response)](1\)Computer-Networks/Communication-paradigms/Publish_Async-Response.md) 
    - [Message queue (async communication):](1\)Computer-Networks/Communication-paradigms/Message_queue_(async communication).md) 
      - Messaging architecture:
        - Broker-less messaging  ✅
        - Broker messaging (Event-driven architecture)  ✅
      - Messaging protocols:
        - Advanced Message Queuing Protocol (AMQP) ✅
        - Message Queue Telemetry Transport (MQTT);
        - Simple/Streaming Text Orientated Messaging Protocol (STOMP);
    - [Transactional messaging patterns:](1\)Computer-Networks/Communication-paradigms/Transactional_messaging_patterns.md)
      - Transactional outbox (database table as a message queue); ✅
      - Transaction log tailing / commit log; ✅
      - Polling publisher; ✅
  
  
## 2) Security:
  - **API security:**
    - **Information security:**
      - [<ins>Access control techniques:</ins>](2\)Security/API-Security/Information-security/Access-control-techniques/Access_control_techniques.md)
        - [Authentication/Authorization token storage/transport](2\)Security/API-Security/Information-security/Access-control-techniques/Authentication-Authorization_token_storage_transport.md); ✅
        - Authentication:
          - [Basic HTTP Authentication](2\)Security/API-Security/Information-security/Access-control-techniques/Authentication/Basic_HTTP_Authentication.md); ✅
          - [Token based Authentication (Bearer token):](2\)Security/API-Security/Information-security/Access-control-techniques/Authentication/Token-based-Authentication-(Bearer token)/Token_based_Authentication_(Bearer-token).md)
            - [Access token (session-id)](2\)Security/API-Security/Information-security/Access-control-techniques/Authentication/Token-based-Authentication-(Bearer token)/Access_token_(session-id).md); ✅
            - [Self-contained token (JWT / JOSE)](2\)Security/API-Security/Information-security/Access-control-techniques/Authentication/Token-based-Authentication-(Bearer token)/Self-contained_token_(JWT).md);  ✅
          - [Open ID Connect Authentication (OAuth 2.0)](2\)Security/API-Security/Information-security/Access-control-techniques/Authentication/Open_ID_Connect_Authentication_(OAuth2.0).md); ✅
        - Authorization:
          - [SSO](2\)Security/API-Security/Information-security/Access-control-techniques/Authorization/SSO.md); ✅
          - [Delegated authorization (OAuth 2.0) + PKCE](2\)Security/API-Security/Information-security/Access-control-techniques/Authorization/Delegated-authorization-(OAuth2.0)+PKCE/index.md);  ✅
      - <ins>Backup and recovery optimization;
      - <ins>Data masking;
      - <ins>Cryptography:</ins>
        - [Symmetric Encryption Methods](2\)Security/API-Security/Information-security/Cryptography/Symmetric_Encryption_Methods.md); ✅
        - [Asymmetric Encryption Methods](2\)Security/API-Security/Information-security/Cryptography/Asymmetric_Encryption_Methods.md); ✅
        - [Hashing Functions](2\)Security/API-Security/Information-security/Cryptography/Hashing_Functions.md); ✅
      - ...
    - **Network security:**
      -  <ins>Firewalls; 
      -  <ins>Load-balancers;
      -  <ins>Reverse proxies;
      -  [<ins>SOP / CORS;</ins>](2\)Security/API-Security/Network-security/SOP_CORS.md) ✅
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
    - [**OWASP**](2\)Security/API-vulnerabilities/OWASP.md); ✅
    - **Injections:**
      - **DB:**
        - [<ins>SQL;</ins>](2\)Security/API-vulnerabilities/Injections/DB/SQL.md) ✅
        - [<ins>NoSQL Injections;</ins>](2\)Security/API-vulnerabilities/Injections/DB/NoSQL.md) ✅
      - **JS:**     
        - [<ins>XSS;</ins>](2\)Security/API-vulnerabilities/Injections/JS/XSS.md) ✅
    - [**Spoofing or tampering token:**](2\)Security/API-vulnerabilities/Spoofing-or-tampering-token/Spoofing_or_tampering_token.md)
      - [**Session token fixation;**](2\)Security/API-vulnerabilities/Spoofing-or-tampering-token/Session_token_fixation.md) ✅
      - [**Injected DB (hashing access token);**](2\)Security/API-vulnerabilities/Spoofing-or-tampering-token/Injected_DB_(hashing_access_token).md) ✅
      - [**Injected client + interception (MAC / HMAC signature);**](2\)Security/API-vulnerabilities/Spoofing-or-tampering-token/Injected_client+interception_(MAC_HMAC_signature).md) ✅
    - [**CSRF;**](2\)Security/API-vulnerabilities/CSRF.md) ✅
    - [**DDoS;**](2\)Security/API-vulnerabilities/DDoS.md) ✅
    - [**Brute force attack;**](2\)Security/API-vulnerabilities/Brute_force_attack.md) ✅
  
## 3) Architecture:
**Link:** https://ru.wikipedia.org/wiki/%D0%A8%D0%B0%D0%B1%D0%BB%D0%BE%D0%BD_%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F

### 3.1) API architectural styles (server - client):
  - [**REST:**](3\)Architecture/3.1\)API-architectural-styles-(server-client)/REST/REST.md)
    - REST-full Principles; ✅
    - HATEOAS; ✅
  - [**RPC:**](3\)Architecture/3.1\)API-architectural-styles-(server-client)/RPC/RPC.md)
    - XML-RPC; ✅
    - JSON-RPC; ✅
    - gRPC; ✅
  - [**GraphQL;**](3\)Architecture/3.1\)API-architectural-styles-(server-client)/GraphQL/GraphQL.md)✅
  - **SOAP;**

### 3.2) Client-Server communication specification:
  - **JSONApi spec;**

### 3.3) Code organization:
  - **Code separation;**
  - **Namespacing;**
  - **Modularity:**  
    - [_modularity:](3\)Architecture/3.3\)Code-organization/Modularity/_modularity.md) ✅
      - сцепленность (cohesion) / связанность (coupling); ✅
      - fine-grained (мелкозернистый) / coarse-grained code (крупнозернистый); ✅
    - [Singleton dependencies;](3\)Architecture/3.3\)Code-organization/Modularity/Singleton_dependencies.md) ✅
    - [Dependency injection;](3\)Architecture/3.3\)Code-organization/Modularity/Dependency_injection.md) ✅
    - [Circular dependencies;](3\)Architecture/3.3\)Code-organization/Modularity/Circular_dependencies.md) ✅
  
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
    - [**Layered (n-tier) architecture pattern;**](3\)Architecture/3.5\)Software-Architectural-pattern/1\)Monolithic-architecture/Layered-(n-tier)-architecture-pattern/Layered_(n-tier)_architecture_pattern.md)✅
    - [**Microkernel (plug-in) Architecture pattern;**](3\)Architecture/3.5\)Software-Architectural-pattern/1\)Monolithic-architecture/Microkernel-(plug-in)-Architecture-pattern:/Microkernel_(plug-in)_Architecture_pattern.md)✅
    - **Pipe-Filter Architecture pattern;**
  - ### Distributed architecture:
    - [**Event-driven architecture pattern;**](3\)Architecture/3.5\)Software-Architectural-pattern/2\)Distributed-architecture/Event-driven-architecture-pattern/Event-driven_architecture_pattern.md)✅
    - [**Microservices architecture pattern:**](3\)Architecture/3.5\)Software-Architectural-pattern/2\)Distributed-architecture/Microservices-architecture-pattern/Microservices_architecture.md)✅
      - **Data management:**  ✅
        - [**<ins>DB management:**](3\)Architecture/3.5\)Software-Architectural-pattern/2\)Distributed-architecture/Microservices-architecture-pattern/Data-management/DB-management/DB_management.md)
          - DB per service;  ✅
          - Shared DB;  ✅
          - Shared DB in each service; ✅
        - [**<ins>Communication principles:**](3\)Architecture/3.5\)Software-Architectural-pattern/2\)Distributed-architecture/Microservices-architecture-pattern/Data-management/Communication-principle/Communication_principle.md)
          - **One-to-one;** ✅
          - **One-to-many;** ✅
          - **Sync communication:**  ✅
            - HTTP-REST; ✅
            - HTTP-gRPC; ✅
          - **Circuit breaker pattern:**
            - API Gateway: ✅
              - Service discovery mechanism (serverless); ✅
            - Backends for frontend; ✅
          - **Async communication (Message queue):**
            - Message; ✅
            - Interaction types; ✅
            - **Message queue:**
              - Broker-less messaging; ✅
              - Broker messaging; ✅
              - Protocols:
                - AMQP; ✅
                - STOMP;
                - MQTT;
        - [**<ins>Distributed transactions:**](3\)Architecture/3.5\)Software-Architectural-pattern/2\)Distributed-architecture/Microservices-architecture-pattern/Data-management/Distributed-transactions/Distributed_transactions.md)
          - **Two-phase commit (2PC);** ✅
          - **SAGA pattern**: ✅
            - Choreography-based saga; 
            - Orchestration-based saga (event bus);
      - [**Deployment Tools:**](3\)Architecture/3.5\)Software-Architectural-pattern/2\)Distributed-architecture/Microservices-architecture-pattern/Deployment_Tools.md)
        - Docker; ✅
        - Kubernetes; ✅
        - Skaffold; ✅
      - [**Deployment Env:**](3\)Architecture/3.5\)Software-Architectural-pattern/2\)Distributed-architecture/Microservices-architecture-pattern/Deployment_Flow.md)
        - SSR vs CSR; ✅
        - Share common logic between services: ✅
          - Repeat files in each service; ✅
          - Common repository; ✅
          - NPM registry; ✅
        - Work flow: ✅
          - Repository types: ✅
            - Monorepository; ✅
            - Repository per service; ✅
          - Deployment flow; ✅
      - [**Security:**](3\)Architecture/3.5\)Software-Architectural-pattern/2\)Distributed-architecture/Microservices-architecture-pattern/Security.md)
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
### 3.6) Utils:
  - **Heartbeat/Health check;**
  - **Long-Pooling;**
  - **Swagger;**

## 4) NodeJS:

  - [**<ins>ENGINE V8:</ins>**](4\)NodeJS/ENGINE-V8/NodeJS.md) 
    - [**Execution context:**](4\)NodeJS/ENGINE-V8/Execution-context/Execution_context.md)
      - Global execution context; ✅
      - Functional execution context; ✅
      - Lexical environment; ✅
    - [**Execution Stack + Heap:**](4\)NodeJS/ENGINE-V8/Execution-Stack-Heap/Execution_Stack_Heap.md) 
      - [JS memory model;](4\)NodeJS/ENGINE-V8/Execution-Stack-Heap/JS_memory_model.md) ✅
    - [**Execution process:**](4\)NodeJS/ENGINE-V8/Execution-process/Execution_process.md) 
      - Parser; ✅
      - Interpreter; ✅
      - JIT Compiler; ✅
    - [**Garbage collector;**](4\)NodeJS/ENGINE-V8/Garbage-collector/Garbage_collector.md)
  - **<ins>LIBUV</ins>:**
    - [Asynchronicity / Event Loop;](4\)NodeJS/Engine-mechanisms/NodeJS/Asynchronicity_Event Loop.md)
    - Thread pool;
  - **<ins>EMBEDDED FUNCTIONALITY:</ins>**
    - **RELP;**
    - **Streams;**
    - **Node's event system:**
      - **Event-driven development;**
      - **Ability to write custom events;**
    - [**Modularity (Require Process);**](4\)NodeJS/Engine-mechanisms/Modularity_(Require_Process).md) ✅

