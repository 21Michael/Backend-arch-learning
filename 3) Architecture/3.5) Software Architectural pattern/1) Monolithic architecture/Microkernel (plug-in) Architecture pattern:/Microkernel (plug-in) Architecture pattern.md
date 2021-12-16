# 3) Microkernel (plug-in) Architecture pattern
Is a natural pattern for implementing **product-based applications.** A product-based 
application is one that is packaged and made available for download in versions as a typical
third-party product. However, many companies also develop and release their internal business 
applications like software products, complete with versions, release notes, and pluggable 
features. These are also a natural fit for this pattern. The microkernel architecture
pattern allows you to **add additional application features as plug-ins to the core application,
providing extensibility as well as feature separation and isolation.**

## Concepts:
![link](https://ebrary.net/htm/img/29/477/21.png)

  - ### Core system:
    The core system of the microkernel architecture pattern traditionally contains only the 
    minimal functionality required to make the system operational. Many operating systems 
    implement the microkernel architecture pattern, hence the origin of this pattern’s name.
    From a business-application perspective, the core system is often defined as the general 
    business logic sans custom code for special cases, special rules, or complex conditional 
    processing.  
    __   
    The core system needs to know about which plug-in modules are available and how to get to
    them. One common way of implementing this is through some sort of **plug-in registry.**    
    __   
    **Registry contains information about each plug-in module, including:**
      - name;
      - data contract (input data and output data);
      - contract format (XML...);
      - remote access protocol details (depending on how the plug-in is connected to the core system;
      - ...
    
  - ### Plug-in modules:
    The plug-in modules are stand-alone, independent components that contain specialized 
    processing, additional features, and custom code that is meant to enhance or extend the core
    system to produce additional business capabilities. Generally, plug-in modules should be
    independent of other plug-in modules, but you can certainly design plug-ins that require 
    other plug-ins to be present. Either way, it is important to keep the communication between
    plug-ins to a minimum to avoid dependency issues.  
    --
    Plug-in modules can be connected to the core system through a variety of ways, including 
    OSGi (open service gateway initiative), messaging, web services, or even direct 
    point-to-point binding...; The architecture pattern itself does not specify any of these 
    implementation details, only that the plug-in modules must remain independent from one another.
    
## Plug-in architecture pros:
  - ### Easy to add new changes
    Changes can largely be isolated and implemented quickly through loosely coupled plug-in modules.
  - ### Easy to test
    Plug-in modules can be tested in isolation.
  - ### Easy to deploy
    Depending on how the pattern is implemented, the plug-in modules can be dynamically added to the core system at runtime.
  - ### High performance
    You can customize and streamline applications to only include those features you need.

## Plug-in architecture cons:
  - ### Low scalability
    Microkernel architecture implementations are product based and are generally smaller in size, they are implemented as single units and hence not highly scalable.
  - ### Difficult to develop
    Requires thoughtful design and contract governance, making it rather complex to implement. Contract versioning, internal plug-in registries, plug-in granularity, and the wide choices available for plug-in connectivity.

## Example:
The stack of folders represents the **core system** for claims processing. It contains the basic
business logic required by the insurance company to process a claim, except without any
custom processing.  
--  
Each **plug-in module** contains the specific rules for that state. In this example, the plug-in
modules can be implemented using custom source code or separate rules engine instances.  
--  
The **key point** is that state-specific rules and processing is separate from the core claims 
system and can be added, removed, and changed with little or no effect on the rest of the core 
system or other plug-in modules.

![link](https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/assets/sapr_0302.png)

## Conclusion:
One great thing about the microkernel architecture pattern is that **<ins>it can be embedded or used 
as part of another architecture pattern.**</ins> For example, if this pattern solves a particular 
problem you have with a specific volatile area of the application, you might find that
you can’t implement the entire architecture using this pattern. In this
case, you can embed the **<ins>microservices architecture pattern in another pattern you are using 
(e.g., layered architecture). Similarly, the event-processor components described in the 
previous section on event-driven architecture could be implemented using the
microservices architecture pattern.**</ins>

|CONCEPT|RATING|ANALISIS|
|-------|------|--------|
|**Overall agility (flexibility)**|High|Overall agility is the ability to respond quickly to a constantly changing environment. Changes can largely be isolated and implemented quickly through loosely coupled plug-in modules. In general, the core system of most microkernel architectures tends to become stable quickly, and as such is fairly robust and requires few changes over time.|
|**Ease of deployment**|High|Depending on how the pattern is implemented, the plug-in modules can be dynamically added to the core system at runtime (e.g., hot-deployed), minimizing downtime during deployment.|
|**Testability**|High|Plug-in modules can be tested in isolation and can be easily mocked by the core system to demonstrate or prototype a particular feature with little or no change to the core system.|
|**Performance**|High|While the microkernel pattern does not naturally lend itself to high-performance applications, in general, most applications built using the microkernel architecture pattern perform well because you can customize and streamline applications to only include those features you need. The JBoss Application Server is a good example of this: with its plug-in architecture, you can trim down the application server to only those features you need, removing expensive non-used features such as remote access, messaging, and caching that consume memory, CPU, and threads and slow down the app server.|
|**Scalability**|Low|Because most microkernel architecture implementations are product based and are generally smaller in size, they are implemented as single units and hence not highly scalable. Depending on how you implement the plug-in modules, you can sometimes provide scalability at the plug-in feature level, but overall this pattern is not known for producing highly scalable applications.|
|**Ease of development**|Low|The microkernel architecture requires thoughtful design and contract governance, making it rather complex to implement. Contract versioning, internal plug-in registries, plug-in granularity, and the wide choices available for plug-in connectivity all contribute to the complexity involved with implementing this pattern.|
