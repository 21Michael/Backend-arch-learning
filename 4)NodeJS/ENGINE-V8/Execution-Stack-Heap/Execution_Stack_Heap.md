# Execution Stack + Heap:
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
