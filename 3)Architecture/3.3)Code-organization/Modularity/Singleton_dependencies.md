# Singleton dependencies

**Singleton dependencies** is a way of importing dependencies from one module to other
by using Singleton pattern that allows to use only one instance of the certain module
for injecting it to different modules;

![link](https://drek4537l1klr.cloudfront.net/prasanna/Figures/05fig10.jpg)

**Example (single DB instance):**
```js
const sqlite3 = require('sqlite3');
const logger = require('../utils/logger/logger');

sqlite3.verbose();

const connectToDB = () => {
  try {
    const db = new sqlite3.Database(':memory:');

    logger.info('Connected to the in-memory SQlite database.');

    return db;
  } catch (err) {
    logger.error(err.message);
  }
};

module.exports = connectToDB();
```

![link](https://drive.google.com/uc?id=1hGW_sFz8-kHvExr1MhuEm0zs8XdPEzG2)