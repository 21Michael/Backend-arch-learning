# Transactional messaging patterns

A service often needs to publish messages as part of a transaction that updates the
database. For instance, throughout this book you see examples of services that publish
domain events whenever they create or update business entities.   
**Both the database update and the sending of the message must happen within a 
transaction. Otherwise, a service might update the database and then crash, for example,
before sending the message. If the service doesn’t perform these two operations 
atomically, a failure could leave the system in an inconsistent state.**

## 1) Transactional outbox (database table as a message queue):

This pattern uses a database table as a temporary message queue. A service that sends
messages has an OUTBOX database table. As part of the database transaction that creates,
updates, and deletes business objects, the service sends messages by inserting them into
the OUTBOX table. Atomicity is guaranteed because this is a local ACID transaction.

The OUTBOX table acts a temporary message queue. **The MessageRelay** is a component that 
reads the OUTBOX table and publishes the messages to a message broker.

![link](https://microservices.io/i/patterns/data/ReliablePublication.png)

Each business entity stored as a record in the database has an attribute that is a list
of messages that need to be published. When a service updates an entity in the database,
it appends a message to that list. This is atomic because it’s done with a single 
database operation. The challenge, though, is efficiently finding those business 
entities that have events and publishing them.
There are a couple of different ways to move messages from the database to the
message broker.

## 2) Polling publisher:
If the application uses a relational database, a very simple way to publish the messages
inserted into the OUTBOX table is for the MessageRelay to poll the table for unpub-
lished messages. It periodically queries the table:

```text
SELECT * FROM OUTBOX ORDERED BY ... ASC
```

Next, the MessageRelay publishes those messages to the message broker, sending one
to its destination message channel. Finally, it deletes those messages from the OUTBOX
table:
```text
BEGIN
  DELETE FROM OUTBOX WHERE ID in (....)
COMMIT
```

**Pros:**
  - Simple approach that works reasonably well at low scale;

**Cons:**
  - Frequently polling the database can be expensive;
  - Whether you can use this approach with a NoSQL database depends on its querying 
    capabilities. That’s because rather than querying an OUTBOX table, the application
    must query the business entities, and that may or may not be possible to do 
    efficiently;
    
## 3) Transaction log tailing / commit log:

A sophisticated solution is for MessageRelay to tail the database transaction log (also
called the commit log). Every committed update made by an application is repre-
sented as an entry in the database’s transaction log. A transaction log miner can read
the transaction log and publish each change as a message to the message broker.

![link](https://microservices.io/i/patterns/data/TransactionLogMining.png)

The Transaction Log Miner reads the transaction log entries. It converts each relevant
log entry corresponding to an inserted message into a message and publishes that mes-
sage to the message broker. This approach can be used to publish messages written to
an OUTBOX table in an RDBMS or messages appended to records in a NoSQL database.

**Tools:** Debezium, LinkedIn Databus, DynamoDB streams, Eventuate Tram;