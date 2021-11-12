# 1) Layered (n-tier) architecture pattern
Layered architecture pattern are organized into horizontal layers, each layer performing a specific role
within the application.  Although the layered architecture pattern **does not specify the number and
types of layers** that must exist in the pattern, most layered architectures consist of four standard

## Basic Layers:
  - ### Presentation;
  - ### Business;
  - ### Persistence;
  - ### Database;

![link](https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/assets/sapr_0101.png)

Smaller applications may have only three layers, whereas larger and more complex business applications may
contain five or more layers. Each layer in the architecture forms an abstraction around the work that needs
to be done to satisfy a particular business request;

## Concepts:
  - ### Closed layer: 
    A closed layer means that as a request moves from layer to layer, it must go through the layer right
    below it to get to the next layer below that one. For example, a request originating from the
    presentation layer must first go through the business layer and then to the persistence layer before
    finally hitting the database layer.
    ![link](https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/assets/sapr_0102.png)

  - ### Layers of isolation:   
    The layers of isolation concept **<ins>means that changes made in one layer of the architecture generally
    don’t impact or affect components in other layers:</ins>** the change is isolated to the components within
    that layer, and possibly another associated layer (such as a persistence layer containing SQL).
    If you allow the presentation layer direct access to the persistence layer, then changes made to SQL
    within the persistence layer would impact both the business layer and the prsentation layer, thereby
    producing a very tightly coupled application with lots of interdependencies between components. This
    type of architecture then becomes very hard and expensive to change.
  
    The layers of isolation concept also means that **<ins>each layer is independent of the other layers,</ins>**
    thereby having little or no knowledge of the inner workings of other layers in the architecture.

  - ### Open layer:
    The services layer in this case is marked as open, meaning requests are allowed to bypass this open
    layer and go directly to the layer below it. In the following example, since the services layer is
    open, the business layer is now allowed to bypass it and go directly to the persistence layer, which
    makes perfect sense.
    ![link](https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/assets/sapr_0103.png)

## Layered architecture pros:
  - ### Separation of concerns among components:
    Components within a specific layer deal only with logic that pertains to that layer. For
    example, components in the presentation layer deal only with presentation logic, whereas components
    residing in the business layer deal only with business logic. This type of component classification
    makes it easy to build effective roles and responsibility models into your architecture, and also
    makes it easy to develop, test, govern, and maintain applications using this architecture pattern
    due to well-defined component interfaces and limited component scope.
  - ### Easy to test
  - ### Easy to deploy
  
## Layered architecture cons:
  - ### Difficult to deploy
  - ### Difficult to scale
  - ### Low performance;

## Example:
![link](https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/assets/sapr_0104.png)

## Conclusion:

|CONCEPT|RATING|ANALISIS|
|-------|------|--------|
|**Overall agility (flexibility)**|Low|Overall agility is the ability to respond quickly to a constantly changing environment. While change can be isolated through the layers of isolation feature of this pattern, it is still cumbersome and time-consuming to make changes in this architecture pattern because of the monolithic nature of most implementations as well as the tight coupling of components usually found with this pattern|
|**Ease of deployment**|Low|Depending on how you implement this pattern, deployment can become an issue, particularly for larger applications. One small change to a component can require a redeployment of the entire application (or a large portion of the application), resulting in deployments that need to be planned, scheduled, and executed during off-hours or on weekends. As such, this pattern does not easily lend itself toward a continuous delivery pipeline, further reducing the overall rating for deployment.|
|**Testability**|High|Because components belong to specific layers in the architecture, other layers can be mocked or stubbed, making this pattern is relatively easy to test. A developer can mock a presentation component or screen to isolate testing within a business component, as well as mock the business layer to test certain screen functionality.|
|**Performance**|Low|While it is true some layered architectures can perform well, the pattern does not lend itself to high-performance applications due to the inefficiencies of having to go through multiple layers of the architecture to fulfill a business request.|
|**Scalability**|Low|Because of the trend toward tightly coupled and monolithic implementations of this pattern, applications build using this architecture pattern are generally difficult to scale. You can scale a layered architecture by splitting the layers into separate physical deployments or replicating the entire application into multiple nodes, but overall the granularity is too broad, making it expensive to scale.|
|**Ease of development**|High|Ease of development gets a relatively high score, mostly because this pattern is so well known and is not overly complex to implement. Because most companies develop applications by separating skill sets by layers (presentation, business, database), this pattern becomes a natural choice for most business-application development. The connection between a company’s communication and organization structure and the way it develops software is outlined is what is called Conway’s law. You can Google “Conway’s law" to get more information about this fascinating correlation.|