# CRUD (Create, Read, Update, and Delete)

**Create, Read, Update, and Delete — or CRUD** — are the four major functions used to 
interact with database applications. The acronym is popular among programmers, as it 
provides a quick reminder of what data manipulation functions are needed for an
application to feel complete.

The CRUD paradigm is common in constructing web applications, because it provides a 
memorable framework for reminding developers of how to construct full, usable models.
Many programming languages and protocols have their own equivalent of CRUD, often 
with slight variations in how the functions are named and what they do. 

**Equivalents:**

|NAME|DESCRIPTION|SQL EQUIVALENT|HTTP EQUIVALENT|
|----|-----------|--------------|---------------|
|CREATE|Adds one or more new entries|INSERT|POST/PUT|
|READ|Retrieves entries that match certain criteria (if there are any)|SELECT|GET|
|UPDATE|Changes specific fields in existing entries|UPDATE|PUT/POST/PATCH|
|DELETE|Entirely removes one or more existing entries|DELETE|DELETE|

In a REST environment, CRUD often corresponds to the HTTP methods POST, GET, PUT, and 
DELETE, respectively. These are the fundamental elements of a persistent storage system.