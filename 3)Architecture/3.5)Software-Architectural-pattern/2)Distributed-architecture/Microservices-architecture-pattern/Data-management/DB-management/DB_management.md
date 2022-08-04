# DB management:

## - DB per service
Keep each microservice’s persistent data private to that service and accessible only via
its API. A service’s transactions only involve its database.

![link](https://microservices.io/i/databaseperservice.png)

The service’s database is effectively part of the implementation of that service. 
It cannot be accessed directly by other services.

There are a few different ways to keep a service’s persistent data private. You do 
not need to provision a database server for each service.   
**For example, if you are using a relational database then the options are:**
  - **Private-tables-per-service** – each service owns a set of tables that must only
    be accessed by that service
  - **Schema-per-service** – each service has a database schema that’s private to that
    service
  - **Database-server-per-service** – each service has it’s own database server.

Private-tables-per-service and schema-per-service have the lowest overhead. Using a 
schema per service is appealing since it makes ownership clearer. Some high throughput 
services might need their own database server.

### Pros:
  - Helps ensure that the services are loosely coupled. Changes to one service’s 
    database does not impact any other services.
  - Each service can use the type of database that is best suited to its needs. For 
    example, a service that does text searches could use ElasticSearch. A service that
    manipulates a social graph could use Neo4j.

### Cons:
  - Implementing business transactions that span multiple services is not straightforward.
    Distributed transactions are best avoided because of the CAP theorem. Moreover, 
    many modern (NoSQL) databases don’t support them.  
    <ins>Solution:</ins>  
      - Saga pattern for transactions;
  - Implementing queries that join data that is now in multiple databases is challenging.  
    <ins>Solution:</ins>
      - API Composition;
      - Command Query Responsibility Segregation (CQRS);
  - Complexity of managing multiple SQL and NoSQL databases.

## - Database replication (Shared DB per service)

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

**Link:** https://jelastic.com/blog/postgresql-auto-clustering-master-slave-replication/

## - Shared DB

Use a (single) database that is shared by multiple services. Each service freely 
accesses data owned by other services using local ACID transactions.

![link](https://dz2cdn1.dzone.com/storage/temp/11241409-figure1.png)

### Pros:
  - A developer uses familiar and straightforward ACID transactions to enforce data 
    consistency;
  - A single database is simpler to operate;

### Cons:
  - **Development time coupling** - a developer working on, for example, the OrderService 
    will need to coordinate schema changes with the developers of other services that 
    access the same tables. This coupling and additional coordination will slow down 
    development.
  - **Runtime coupling** - because all services access the same database they can potentially
    interfere with one another. For example, if long running CustomerService 
    transaction holds a lock on the ORDER table then the OrderService will be blocked.
  - Single database might not satisfy the data storage and access requirements of all 
    services.
    