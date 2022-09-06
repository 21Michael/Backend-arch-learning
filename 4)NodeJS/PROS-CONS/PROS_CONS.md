# PROS / CONS
### <ins>PROS</ins>:
  - **Asynchronicity / Non-blocking (Even Loop + Thread Pool);**
  - **Event driven;**
  - **Easy to implement Microservices;**
  - **Multi aims language:**
      - different platforms;
      - front-end;
      - different OS;
  - **High Performance (Interpreter + JIT);**
  - **Large community;**
  - **npm;**

### <ins>CONS</ins>:
  - **Asynchronicity / blocking** (single thread and event loop can be blocked);  
    <ins>Preventive measures:</ins> use `async hooks` for measuring async tasks process time.  
    https://medium.com/voodoo-engineering/node-js-lots-of-ways-to-block-your-event-loop-and-how-to-avoid-it-b41f41deecf5
  - **High Performance** (single thread);  
    <ins>Preventive measures:</ins> run heavy tasks in separate thread. Use `worker thread` for them;
  - **npm** (security);  
    <ins>Preventive measures:</ins> use popular libs that is supported and use npm audit
    script;
