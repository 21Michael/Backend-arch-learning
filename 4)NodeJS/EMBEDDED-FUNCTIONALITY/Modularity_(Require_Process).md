# Modularity (Require Process)

## Module Caching:
Node.js caches modules after the first time they are loaded.  
**<ins>For example:</ins>** every call to require(‘foo’) will get exactly the same
object returned, if it would resolve to the same file.
```js
// app-singleton.js

const counter1 = require('./counter.js');
const counter2 = require('./counter.js');

counter1.increment()
counter1.increment()
counter2.increment()

console.log(counter1.get()) // prints 3
console.log(counter2.get()) // also prints 3
```

Node.js modules can behave like **Singletons**, but they are not guaranteed to be always 
singleton. 

**There are two reasons for this:**
  - **Node’s module caching mechanism is case-sensitive;**  
        __   
    **<ins>For example:</ins>** require(‘./foo’) and require(‘./FOO’) return two different objects, 
    irrespective of whether or not ./foo and ./FOO are the same file.
    ```js
    // app-no-singleton-1.js
    const counter1 = require('./counter.js')
    const counter2 = require('./COUNTER.js')
    
    counter1.increment()
    console.log(counter1.get()) // prints 1
    console.log(counter2.get()) // prints 0, not same object as counter1
    
    /*
    We have two different resolved filenames:
    - “Users/laz/repos/medium/modules/counter.js”
    - “Users/laz/repos/medium/modules/COUNTER.js”
      */
    ```
  - **Modules are cached based on their resolved filename (NPM 2.0);**  
         __   
    When file is found, it is then loaded as module and also cached by using its 
    filename as **cache key.**  
    __   
    **<ins>For example:</ins>** Since modules may resolve to a different filename based on the 
    location of the calling module (loading from node_modules folders), it is not a 
    guarantee that require(‘foo’) will always return the exact same object, if it 
    would resolve to different files.
    ```
    // npm2 installed dependencies in nested way
    app.js
    package.json
    node_modules/
    |---module-a/index.js
    |---module-b/index.js
    |---node_modules
    |---module-a/index.js
    ```
    Request:
    ```js
    // app.js
    const moduleA = require(‘module-a’)
    loads: “/node_modules/module-a/index.js”
    
    // /node_modules/module-b/index.js
    const moduleA = require(‘module-a’)
    loads “/node_modules/module-b/node_modules/module-a/index.js”
    ```