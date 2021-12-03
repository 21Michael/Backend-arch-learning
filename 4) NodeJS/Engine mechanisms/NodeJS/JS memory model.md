# JS memory model
**Link:** https://medium.com/@ethannam/javascripts-memory-model-7c972cd2c239

## Data types:
  - ### Primitives
    ### Memory allocation:
    ```js
    let myNumber = 23
    ```
    `1.` **Create a unique identifier for your variable (“myNumber”).**  
    `2.` **Allocate an address in memory (will be assigned at runtime).**  
    `3.` **Store a value at the address allocated.**  
    ![link](https://miro.medium.com/max/1050/1*IiejRUFbks-TaOzJJvdoVw.jpeg)
    `4.` **Assigning the variable to the new variable:**  
    ```js
    let newVar = myNumber;
    ```
    ![link](https://miro.medium.com/max/1050/1*AaUqtuwa2BZiI73bV9RHmA.jpeg)
    `5.` **Reassigning the value:**  
    Primitive data types in JS are immutable, when “myNumber + 1” resolves to “24”, JS
    will allocate a new address in memory, store 24 as its value, and “myNumber” will 
    point to the new address.
    ```js
    myNumber = myNumber + 1
    ```
    ![link](https://miro.medium.com/max/1050/1*awL1xpr8cDNV7AaxiaA7YQ.jpeg)
    ### JS Memory storage:
    The **call stack** is where primitives are stored (in addition to function calls):
    ![link](https://miro.medium.com/max/1050/1*E5Y5QBkntO31o4Al2-_YOA.jpeg)
  - ### Non-primitives
    ### Memory allocation:
    `1.` **Create a unique identifier for your variable (“myArray”).**  
    ```js
      let myArray = []
    ```
    `2.` **Allocate an address in memory (will be assigned at runtime).**   
    `3.` **Store a value of a memory address allocated on the heap (will be assigned 
    at runtime).**   
    `4.` **The memory address on the heap stores the value assigned (the empty array 
    []).**   
    ![link](https://miro.medium.com/max/1050/1*CPnnVIgE0tQVbxIja_C-_A.jpeg)
    `5.` **Push/pop new values to the non-primitive.**
    ```js
    myArray.push("first")
    myArray.push("second")
    myArray.push("third")
    myArray.push("fourth")
    myArray.pop()
    ```
    ![link](https://miro.medium.com/max/1050/1*XfqW2Xh5oJrChzhRAauf9Q.jpeg)
    ### JS Memory storage:
    **The heap** is where non-primitives are stored. The key difference is that the heap 
    can store unordered data that can grow dynamically—perfect for arrays and objects.
    ![link](https://miro.medium.com/max/1050/1*pk7aiCJv3iR2qPMvFpqFLw.jpeg)