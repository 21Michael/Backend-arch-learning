# NodeJS
**Node или Node.js** — программная платформа, основанная на движке V8 (транслирующем JavaScript в машинный код), 
превращающая JavaScript из узкоспециализированного языка в язык общего назначения. Node.js добавляет возможность
JavaScript взаимодействовать с устройствами ввода-вывода через свой API, написанный на C++, подключать другие 
внешние библиотеки, написанные на разных языках, обеспечивая вызовы к ним из JavaScript-кода.

![link](https://drive.google.com/uc?id=10UoF5-507drC7FqmOSX1Rv1tBVqDULHd)

# 1) Engine V8:
**V8 Engine** is an open-source JavaScript engine build using C++. It was built for the Chromium 
Project & the Chrome browsers, but nowadays, it is the base for other JavaScript-based technologies 
like Node.js, MongoDB, etc.

**V8 Engine** is a stand-alone project that is complete in itself as a JS engine. It has no dependency 
on the Chrome browser or anything like that.

![link](https://miro.medium.com/max/1019/1*ZIH_wjqDfZn6NRKsDi9mvA.png)

## 1.1) Execution context:
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
    
  - ## Lexical environment;
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

## 1.3) Execution Stack + Heap:
Execution stack, also known as “calling stack” in other programming languages, is a stack with a **LIFO** 
(Last in, First out) **data structure**, which is used to store all the execution context created during the code
execution.

When the JavaScript engine first encounters your script, it creates a **global execution context** and pushes
it to the current **execution stack.** Whenever the engine finds a function invocation, it creates a new execution
context for that function and pushes it to the top of the stack.

The engine **executes the function whose execution context** is at the top of the stack. When this function 
completes, its execution stack is popped off from the stack, and the control reaches to the context below 
it in the current stack.
![link](https://miro.medium.com/max/2000/1*ACtBy8CIepVTOSYcVwZ34Q.png)

## 1.2) Execution process:
**Link:** https://github.com/21Michael/JS-arch-learning/blob/main/JavaScript/6)%20Optimization%20techniques/Language-specific%20optimizations/JIT/JIT.md

  - ## Parser;
  - ## Interpreter;
  - ## JIT Compiler;

## 1.3) Garbage collector

# 2) libuv:
  - ## Event Loop;
  - ## Thread pool;

# 3) Execution flow:

![link](https://drive.google.com/uc?id=149dxHJbkHUn4zmr4YxA23b71ViRowKmH)