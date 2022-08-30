# 5) Microservices architecture pattern
The microservices architecture style naturally evolved from two main sources: **<ins>monolithic
applications</ins>** developed using the layered architecture pattern and distributed applications
developed through the **<ins>service-oriented architecture pattern.</ins>**  

**Monolithic applications** typically consist of tightly coupled components that are part of a 
single deployable unit, making it cumbersome and difficult to change, test, and deploy the 
application (hence the rise of the common “monthly deployment” cycles typically found in most 
large IT shops). These factors commonly lead to brittle applications that break every time 
something new is deployed.  

**The microservices architecture pattern** addresses these issues by 
separating the application into multiple deployable units (service components) that can be
individually developed, tested, and deployed independent of other service components.  

While the **service-oriented architecture pattern (SOA)** pattern is very powerful and offers 
unparalleled levels of abstraction, heterogeneous connectivity, service orchestration, and the promise
of aligning business goals with IT capabilities, it is nevertheless com‐plex, expensive, 
ubiquitous, difficult to understand and implement, and is usually overkill for most applications.  

**The microservices architecture style** addresses this complexity by simplifying the notion of a
service, eliminating orchestration needs, and simplifying connectivity and access to service 
components.

## Concepts:
  - ### Separately deployed units:
    Each component of the microservices architecture is deployed as a separate unit, allowing
    for easier deployment through an effective and streamlined delivery pipeline, increased 
    scalability, and a high degree of application and component decoupling within your 
    application.
    
  - ### Service component:
    Service components contain one or more modules (e.g., Java classes) that represent either
    a single-purpose function (e.g., providing the weather for a specific city or town) or an 
    independent portion of a large business application (e.g., stock trade placement or
    determining auto-insurance rates). Designing the right level of service component 
    granularity is one of the biggest challenges.
    
  - ### Distributed (распределенная) architecture:
    Meaning that all the components within the architecture are fully decoupled from one other
    and accessed through some sort of remote access protocol (JMS, AMQP, REST, SOAP, RMI, etc.).
    The distributed nature of this architecture pattern is how it achieves some of its superior
    scalability and deployment characteristics.
    

## Topologies (ways to implement a microservices architecture pattern):
  - ### API REST-based topology:
    Useful for websites that expose small, self-contained individual services through some 
    sort of API (application programming interface). This topology consists of very fine-grained
    service components (hence the name microservices) that contain one or two
    modules that perform specific business functions independent from the rest of the services. 
    In this topology, these fine-grained service components are typically accessed using a 
    REST-based interface implemented through a separately deployed web-based API layer.
    
    ![link](https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/assets/sapr_0402.png)
    
  - ### Application REST-based topology:
    Differs from the API REST-based approach in that client requests are received through 
    traditional web-based or fat-client business application screens rather than through a simple
    API layer. As illustrated in Figure 4-3, the user-interface layer of the application is 
    deployed as a separate web application that remotely accesses separately deployed service 
    components (business functionality) through simple REST-based interfaces. The service 
    components in this topology differ from those in the API-REST-based topology in that these 
    service components tend to be larger, more coarse-grained, and represent a small portion of
    the overall business application rather than fine-grained, single-action services. 
    This topology is common for **small to medium-sized** business applications that have a relatively low degree of complexity.
    
    ![link](https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/assets/sapr_0403.png)
    
  - ### Centralized messaging topology:
    Similar to the previous application REST-based topology except that instead of using REST 
    for remote access, this topology uses a **lightweight centralized message broker (e.g.,
    RabbitMQ, Kafka, Redis, etc.).** It is vitally important when looking at this topology not
    to confuse it with the service-oriented architecture pattern or consider it “SOA-Lite."   
    __   
    **<ins>The lightweight message broker / Event bus</ins>** found in this topology does not perform any orchestration,
    transformation, or complex routing; rather, it is just a lightweight transport to access 
    remote service components.    
    
    ![link](https://drive.google.com/uc?id=1xM1x0M6g9IoVLP6onZrIyV5lYYIwA7zL)
    __   
    The centralized messaging topology is typically found in **<ins>larger business applications</ins>** or
    applications requiring more sophisticated control over the transport layer between the user
    interface and the service components. The benefits of this topology over the simple
    REST-based topology discussed previously are advanced queuing mechanisms, asynchronous 
    messaging, monitoring, error handling, and better overall load balancing and scalability.
    The single point of failure and architectural bottleneck issues usually associated with a
    centralized broker are addressed through broker clustering and broker federation (splitting
    a single broker instance into multiple broker instances to divide the message throughput 
    load based on functional areas of the system).
    
    ![link](https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/assets/sapr_0404.png)

## Microservices pattern potholes:
  - ### Determining the correct level of granularity (детализации) or the service components:
    - **The problem: <ins>too coarse-grained (высокоуровневые абстракции / крупнозернистые):</ins>**  larger components
      than fine-grained, large subcomponents. Simply wraps one or more fine-grained services 
      together into a more coarse-grained operation.   
      If service components are too coarse-grained you may not realize the benefits that come 
      with this architecture pattern (deployment, scalability, testability, and loose coupling).
      If you find you need to orchestrate your service components from within the **user interface 
      or API layer of the application,** then chances are your service components are too 
      coarse-grained.
      
    - **The problem: <ins>too fine-grained (низкоуровневые абстракции / мелкозернистые):</ins>**
      smaller components of which the larger ones are composed, lower-level service.
      If services too fine-grained will lead to service orchestration requirements,
      which will quickly turn your lean microservices architecture into a heavyweight 
      service-oriented architecture, complete with all the complexity, confusion, expense, and
      fluff typically found with SOA-based applications.  
        - **The problem: <ins>inter-service communication between service components:</ins>**
            - **Shared data** (Service 1 needs data from DB of Service 2 and Service 3);
            - **Shared logic** (Service 1 needs logic from Service 2 and Service 3);  
          
          If you find you need to perform **inter-service communication between service components**
          to process a single request, chances are your service components are either too fine-grained
          or they are not partitioned correctly from a business functionality standpoint.
          
          ![link](https://drive.google.com/uc?id=1fBKJYzcRwPSKqoLJj3tHCXe8YoHXo8_5)
          
          Inter-service communication, which could force undesired couplings between components,
          can be handled instead through a **shared database.**
          
        - **The solution 1 (cannot scale an individual component): <ins>Shared DB / logic:</ins>**   
          When these services have a single monolithic shared database, it is very difficult 
          to scale the database based on the traffic spike. This design pattern is common with
          traditional applications where data is often shared between various components. 
          However, the tight coupling between the services will be a hindrance to deploying 
          service changes independently. The only option you have is to scale out the entire 
          monolithic database – you cannot scale an individual component.
          
          ![link](https://drive.google.com/uc?id=1e4_Qo05VkYmOIAOb5jMI9oJKdk4TKHDI)
          
          For example, if a service component handing Internet orders needs customer information,
          it can go to the database to retrieve the necessary data as opposed to invoking
          functionality within the customer-service component.  
          Same solution also works and for logic that can be saved in scripts in decoupled 
          repository or NPM registry.

        - **The solution 2 (doesn't follow DRY principle): <ins>Repeating shared data and 
          logic in each service:</ins>**  
          Because of cheap DB memory we can afford to make copies by the same DB in each 
          service, but now we have to maintain consistency (согласованность) between DB in 
          each server by using transactions.  
          If a service component needs functionality contained within another service 
          component or common to all service components, you can sometimes copy the shared
          functionality across service components (thereby violating the DRY principle: 
          don’t repeat yourself). This is a fairly common practice in most business 
          applications implementing the microservices architecture pattern, trading off the
          redundancy of repeating small portions of business logic for the sake of keeping
          service components independent and separating their deployment. Small utility
          classes might fall into this category of repeated code.
          
          ![link](https://drive.google.com/uc?id=1REMorKjrFshdwUzaswWlqAPusiJFL4Ag)
          
    - **The solution (difficult to implement): <ins>compose coarse-grained services with 
      fine-grained operations:</ins>**  
      Using both levels of abstractions simultaneously allows architecting proper granularity
      of services by business logic or abstraction by it's very difficult to achieve.
      
      ![link](https://i.stack.imgur.com/e9PKw.jpg)
    
## Microservices architecture pros:
  - ### High flexibility
    Due to the notion of separately deployed units, change is generally isolated to individual
    service components, which allows for fast and easy deployment. Also, applications build 
    using this pattern tend to be very loosely coupled, which also helps facilitate change.
  - ### Easy to deploy
    Microservice typically have small codebases, making them easier to maintain and deploy. 
    It’s also much easier to keep the code clean and for teams to be wholly responsible for 
    specific services.
  - ### Easy to test
    Due to the separation and isolation of business functionality into independent
    applications, testing can be scoped, allowing for more targeted testing efforts.
  - ### Easy to scale
    Because the application is split into separately deployed units, each service component 
    can be individually scaled, allowing for fine-tuned scaling of the application.
  - ### Easy to develop
    Because functionality is isolated into separate and distinct service components, 
    development becomes easier due to the smaller and isolated scope.
## Microservices architecture cons:
  - ### Low performance
    While you can create applications implemented from this pattern that perform very well, 
    overall this pattern does not naturally lend itself to high-performance applications due
    to the distributed nature of the microservices architecture pattern.
  - ### Difficult to develop architecture

## Conclusion:
The microservices architecture pattern solves many of the common issues found in both 
monolithic applications as well as service-oriented architectures. Since major application 
components are split up into smaller, separately deployed units, applications built
using the microservices architecture pattern are generally more robust, provide better 
scalability, and can more easily support continuous delivery.  

Another advantage of this pattern is that it provides the capability to do real-time production
deployments, thereby significantly reducing the need for the traditional monthly or weekend
“big bang” production deployments. Since change is generally isolated to specific service 
components, only the service components that change need to be deployed. If you only have a 
single instance of a service component, you can write specialized code in the user interface 
application to detect an active hot-deployment and redirect users to an error page or waiting
page. Alternatively, you can swap multiple instances of a service component in and out during
a real-time deployment, allowing for continuous availability during deployment
cycles (something that is very difficult to do with the layered architecture pattern).

One final consideration to take into account is that since the micro‐services architecture 
pattern is a distributed architecture, it shares some of the same complex issues found in the
event-driven architecture pattern, including contract creation, maintenance, and government,
remote system availability, and remote access authentication and authorization.

|CONCEPT|RATING|ANALISIS|
|-------|------|--------|
|**Overall agility (flexibility)**|High|Overall agility is the ability to respond quickly to a constantly changing environment. Due to the notion of separately deployed units, change is generally isolated to individual service components, which allows for fast and easy deployment. Also, applications build using this pattern tend to be very loosely coupled, which also helps facilitate change.|
|**Ease of deployment**|High| Microservice typically have small codebase, making them easier to maintain and deploy. It’s also much easier to keep the code clean and for teams to be wholly responsible for specific services.|
|**Testability**|High| Due to the separation and isolation of business functionality into independent applications, testing can be scoped, allowing for more targeted testing efforts. Regression testing for a particular service component is much easier and more feasible than regression testing for an entire monolithic application. Also, since the service components in this pattern are loosely coupled, there is much less of a chance from a development perspective of making a change that breaks another part of the application, easing the testing burden of having to test the entire application for one small change.|
|**Performance**|Low|While you can create applications implemented from this pattern that perform very well, overall this pattern does not naturally lend itself to high-performance applications due to the distributed nature of the microservices architecture pattern.|
|**Scalability**|High| Because the application is split into separately deployed units, each service component can be individually scaled, allowing for fine-tuned scaling of the application. For example, the admin area of a stock-trading application may not need to scale due to the low user volumes for that functionality, but the trade-placement service component may need to scale due to the high throughput needed by most trading applications for this functionality.|
|**Ease of development**|High|Because functionality is isolated into separate and distinct service components, development becomes easier due to the smaller and isolated scope. There is much less chance a developer will make a change in one service component that would affect other service components, thereby reducing the coordination needed among developers or development teams.|

![link](https://microservices.io/i/PatternsRelatedToMicroservices.jpg)
