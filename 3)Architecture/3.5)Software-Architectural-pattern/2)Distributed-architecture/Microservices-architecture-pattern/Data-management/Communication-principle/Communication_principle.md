# Communication principles:

![link](https://drive.google.com/uc?id=1KGF2aL7Dam1hSONFWpH2t_BJoEbom04y)

## <ins>Interaction styles:

### 1) One-to-one
```text
Each client request is processed by exactly one service;
```

**Sync:**
  - **Request/response:**   
    A service client makes a request to a service and waits for a response. The client expects the
    response to arrive in a timely fashion. It might event block while waiting. This is an 
    interaction style that generally results in services being tightly coupled.
    
![link](https://i0.wp.com/www.dineshonjava.com/wp-content/uploads/2019/05/one-to-one-sync.png?w=612&ssl=1)


**Async:**
  - **Request/response:**  
    A service client sends a request to a service, which replies asynchronously. The client 
    doesn’t block while waiting, because the service might not send the response for a long time.
  - **One-way notifications:**  
    A service client sends a request to a service, but no reply is expected or sent.

![link](https://i1.wp.com/www.dineshonjava.com/wp-content/uploads/2019/05/asynchronous-one-to-one.png?w=607&ssl=1)

### 2) One-to-many
```text
Each request is processed by multiple services.
```
**Async:**
  - **Publish/subscribe:**   
    A client publishes a notification message, which is consumed by zero or more interested 
    services.
  - **Publish/async responses:**  
    A client publishes a request message and then waits for a certain amount of time for 
    responses from interested services.

![link](https://i2.wp.com/www.dineshonjava.com/wp-content/uploads/2019/05/asynchronous-one-to-many.png?w=586&ssl=1)
## <ins>Interaction types:

### 1) Sync communication:
When using a remote procedure invocation-based IPC mechanism, a client sends a
request to a service, and the service processes the request and sends back a response.
Some clients may block waiting for a response, and others might have a reactive, non-
blocking architecture. But unlike when using messaging, the client assumes that the
response will arrive in a timely fashion.

![link](https://drive.google.com/uc?id=17FKRQAWavkHQwHEAXpN7xRyXOTn4Cagd)

- **<h3>HTTP-REST</h3>**  
  REST provides a set of architectural constraints that, when applied as a whole, emphasizes
  scalability of component interactions, generality of interfaces, independent deployment of
  components, and intermediary components to reduce interaction latency, enforce security,
  and encapsulate legacy systems.  
  
  ![link](http://microservices.io/i/Microservice_Architecture.png)
  
  **Pros:**  
    - It’s simple and familiar.
    - You can test an HTTP API from within a browser using, for example, the Postman plugin, or
      from the command line using curl (assuming JSON or some other text format is used).
    - It directly supports request/response style communication.
    - HTTP is, of course, firewall friendly.
    - It doesn’t require an intermediate broker, which simplifies the system’s architecture.
    
  **Cons:**
    - It only supports the request/response style of communication.
    - Reduced availability. Because the client and service communicate directly without an 
      intermediary to buffer messages, they must both be running for the duration of the exchange. 
    - Clients must know the locations (URLs) of the service instances(s). Clients must
      use what is known as a service discovery mechanism to locate service instances.
    - Fetching multiple resources in a single request is challenging.
    - It’s sometimes difficult to map multiple update operations to HTTP verbs.
    
- **<h3>HTTP-gRPC</h3>**  
  **gRPC** - is a binary message-based protocol, this means you’re forced to take an API-first
  approach to service design. You define your gRPC APIs using a Protocol Buffers-based
  IDL, which is Google’s language-neutral mechanism for serializing structured data.
  You use the Protocol Buffer compiler to generate client-side stubs and server-side skeletons.  
  Clients and servers exchange binary messages in the **Protocol Buffers format using HTTP/2**.    
  **A gRPC API consists of one or more services and request/response message definitions.**
  
  ![link](https://techdozo.dev/wp-content/uploads/2021/08/grpc.png)
  
  **Pros:**
    - It’s straightforward to design an API that has a rich set of update operations.
    - It has an efficient, compact IPC mechanism, especially when exchanging large messages.
    - Bidirectional streaming enables both RPI and messaging styles of communication.
    - It enables interoperability between clients and services written in a wide range of 
      languages.  
      
  **Cons:**
    - It takes more work for JavaScript clients to consume gRPC-based API than REST/JSON-based 
      APIs.
    - Older firewalls might not support HTTP/2.
  
### 2) Async communication (Message broker):
When using messaging, services communicate by asynchronously exchanging mes-
sages. A messaging-based application typically uses a message broker, which acts as an
intermediary between the services, although another option is to use a brokerless
architecture, where the services communicate directly with each other. A service client
makes a request to a service by sending it a message. If the service instance is expected
to reply, it will do so by sending a separate message back to the client. Because the
communication is asynchronous, the client doesn’t block waiting for a reply. Instead,
the client is written assuming that the reply won’t be received immediately.

![link](https://drive.google.com/uc?id=1C9uFbjk_vbTCBQyO70mt6MtZVVWcbHZo)

### - <ins>Interaction types:

### 1) Message:
**Link:** https://github.com/21Michael/Backend-arch-learning/blob/main/1)%20Computer%20Networks/Communication%20paradigms/Messages.md

### 2) Request / Response and Asynchronous Request / Response:
**Link:** https://github.com/21Michael/Backend-arch-learning/blob/main/1)%20Computer%20Networks/Communication%20paradigms/Request-Response.md

### 3) One-way notifications:
**Link:**

### 4) Publish / Subscribe:
**Link:** https://github.com/21Michael/Backend-arch-learning/blob/main/1)%20Computer%20Networks/Communication%20paradigms/Publisher-Subscriber.md

### 5) Publish / Async-Response:
**Link:**

### - <ins>Message broker:
**Link:** https://github.com/21Michael/Backend-arch-learning/blob/main/1)%20Computer%20Networks/Communication%20paradigms/Message%20queue%20(async%20communication).md

## **<h3>Circuit breaker patterns:</h3>** 
  
**<ins>The Problem:**
In a distributed system, whenever a service makes a synchronous request to another
service, there is an ever-present risk of partial failure. Because the client and the service
are separate processes, a service may not be able to respond in a timely way to a client’s
request.
 - The service could be down because of a failure or for maintenance.
 - Or the service might be overloaded and responding extremely slowly to requests.

```text
Because the client is blocked waiting for a response, the danger is that the failure
could cascade to the client’s clients and so on and cause an outage.
```
**<ins>The solution:** 
  - **<h3>API Gateway:**</h3> 
    Implement an API gateway that is the single entry point for all clients. The API gateway 
    handles requests in one of two ways. Some requests are simply proxied/routed to the 
    appropriate service. It handles other requests by fanning out to multiple services.
    ![link](https://microservices.io/i/apigateway.jpg)
    
    **Functions:**
      - **One-end point:**  
        The granularity of APIs provided by microservices is often different than what a 
        client needs. Microservices typically provide fine-grained APIs, which means that 
        clients need to interact with multiple services. For example, as described above, 
        a client needing the details for a product needs to fetch data from numerous services.
      - **Network timeouts:**  
        Never block indefinitely and always use timeouts when waiting for a response. Using 
        timeouts ensures that resources are never tied up indefinitely.
      - **Data normalization:**  
        Different clients need different data. For example, the desktop browser version of a 
        product details page desktop is typically more elaborate then the mobile version.
      - **Limiting the number of outstanding requests from a client to a service:**  
        Impose an upper bound on the number of outstanding requests that a client can make to
        a particular service. If the limit has been reached, it’s probably pointless to make
        additional requests, and those attempts should fail immediately.
      - **Circuit breaker pattern:**  
        Track the number of successful and failed requests,
        and if the error rate exceeds some threshold, trip the circuit breaker so that
        further attempts fail immediately. A large number of requests failing suggests
        that the service is unavailable and that sending more requests is pointless.
        After a timeout period, the client should try again, and, if successful, close the
        circuit breaker.
      - **Diverse set of protocols:**   
        Services might use a diverse set of protocols, some of which might not be web friendly.
      - **Additional security layer:**  
        The API gateway might also implement security, e.g. verify that the client is authorized
        to perform the request
      - **Service discovery mechanism (for serverless services):**  
        The service discovery mechanism updates the service registry when service instances
        start and stop. When a client invokes a service, the service discovery mechanism que-
        ries the service registry to obtain a list of available service instances and routes the
        request to one of them.
        
        **Service discovery patterns:**
          - **Self registration:**  
            A service instance invokes the service registry’s registration API to register 
            its network location. It may also supply a health check URL.  
            **The health check** URL is an API end-point that the service 
            registry invokes periodically to verify that the service instance is healthy and 
            available to handle requests. A service registry may require a service instance
            to periodically invoke a **“heartbeat”** API in order to prevent its registration
            from expiring.
            ![link](https://drive.google.com/uc?id=1t5IZd6lJH9qybKm5bSu8i00v2d-9YYvd)
          - **Client-side discovery:**  
            When a service client wants to invoke a service, it queries the service registry to
            obtain a list of the service’s instances. To improve performance, a client might cache
            the service instances. The service client then uses a load-balancing algorithm, such as
            a round-robin or random, to select a service instance. It then makes a request to 
            a select service instance.
            **Docker and Kubernetes** have a built-in service registry and service discovery mecha-
            nism. The deployment platform gives each service a DNS name, a virtual IP (VIP)
            address, and a DNS name that resolves to the VIP address. A service client makes a
            request to the DNS name/VIP, and the deployment platform automatically routes the
            request to one of the available service instances. As a result, service registration, ser-
            vice discovery, and request routing are entirely handled by the deployment platform
            ![link](https://drive.google.com/uc?id=18o8uKRbxcaEW2Sm5Aokzronfjjn7RZ--)
            **This approach is a combination of two patterns:**  
              - **3rd party registration pattern**  
                Instead of a service registering itself with the service registry, a third 
                party called the registrar, which is typically part of the deployment platform,
                handles the registration.
              - **Server-side discovery pattern**  
                Instead of a client querying the service registry, it makes a request to a DNS
                name, which resolves to a request router that queries the service registry and
                load balances requests.

  - <h3>**Backends for frontend:**</h3>  
    A variation of this pattern is the Backends for frontends pattern. It defines a separate
    API gateway for each kind of client. In this example, there are three kinds of clients: 
    web application, mobile application, and external 3rd party application. There are three
    different API gateways. Each one is provides an API for its client.
    ![link](https://microservices.io/i/bffe.png)
    
**Pros (API gateway):**
  - Insulates the clients from how the application is partitioned into microservices;
  - Insulates the clients from the problem of determining the locations of service instances;
  - Provides the optimal API for each client;
  - Reduces the number of requests/roundtrips. For example, the API gateway enables clients to
    retrieve data from multiple services with a single round-trip. Fewer requests also means 
    less overhead and improves the user experience. An API gateway is essential for mobile 
    applications;
  - Simplifies the client by moving logic for calling multiple services from the client to
    API gateway;
  - Translates from a “standard” public web-friendly API protocol to whatever protocols are 
    used internally;

**Cons (API gateway):**
  - Increased complexity - the API gateway is yet another moving part that must be 
    developed, deployed and managed
  - Increased response time due to the additional network hop through the API gateway
  - however, for most applications the cost of an extra roundtrip is insignificant.
