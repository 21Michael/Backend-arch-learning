# NoSQL INJECTION
While NoSQL database engines have a different structure and do not support SQL statements
and SQL queries, they still let users perform queries. They do not support one standardized
language and therefore the query language is dependent on the implementation: database 
(e.g. MongoDB, Redis, Google Cloud Datastore, etc.), language (e.g. Python, PHP, etc.),
and framework (e.g. Node.js, Angular). However, NoSQL queries are most often based on 
JSON and they can include user input. If this input is not sanitized, they are vulnerable
to injections.

## Types:
  - **The injection of tautologies in conditional statements to generate ‘always true’ 
    expressions and bypass access mechanisms:**
  - **The injection of UNION queries to extract unexpected datasets:**
  - **JavaScript injections to run arbitrary code in the database engine:**
  - **Injecting new queries by inserting additional code through special characters:**

## Example:
### Unsafe MongoDB query:
```js
Users.findOne(
  {
    "name" : req.body.name, 
    "password" : req.body.password
  }
 );
```
### Injection:
Instead of sending the intended name and password strings, the injection can be performed
by sending a JSON object containing MongoDB query operators.
```js
{
  "name": { "$ne": "1"},
  "password": { "$ne": "1"}
}
```
The query operator `$ne` (not equal) will be used by the `Users.findOne()` to find the first
User that has a name and password that is not equal to the string `"1"`. Since the 
statement is true and always returns a valid user, this request enables the attacker
to log in without providing the credentials.

## Preventing mechanisms (same as for SQL):
![link](https://drive.google.com/uc?id=1aqjnjy59yzcNEJoUSyT0vv6H7rf_q2Wh)