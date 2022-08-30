# Execution context:
**Execution context** is an abstract concept of an environment where the Javascript code is evaluated and
executed. Whenever any code is run in JavaScript, it’s run inside an execution context.

![link](https://assets.htmlacademy.ru/img/blog/195/global-execution-context@1x.png)

  - ## Global Execution Context
    **Global Execution Context** — This is the default or base execution context. The code that is not inside
    any function is in the global execution context. It performs two things: it creates a global object which 
    is a window object (in the case of browsers) and sets the value of this to equal to the global object. 
    There can only be one global execution context in a program.

  - ## Functional Execution Context
    **Functional Execution Context** — Every time a function is invoked, a brand new execution context is 
    created for that function. Each function has its own execution context, but it’s created when the function
    is invoked or called. There can be any number of function execution contexts. Whenever a new execution 
    context is created, it goes through a series of steps in a defined order which I will discuss later in
    this article.
    
  - ## Lexical environment (Inner Execution Context + outer scope = Closure);
    Every execution context has a reference to its outer environment, and that outer environment is 
    called **Lexical Environment.**
    ```js
        function one(){
          function two(){
            console.log(a);
          };
        
          var a = 2;
          console.log(a);
          two();
        }
        
        var a = 1;
        
        console.log(a);
        one();
    ```
    
    ![link](https://miro.medium.com/max/875/1*ZeBDEb3BrCJVTSe9CPn1jA.jpeg)

