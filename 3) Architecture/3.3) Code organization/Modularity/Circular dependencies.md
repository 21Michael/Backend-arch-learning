# Circular dependencies

In software engineering, a **circular dependency** is a relation between two or more
modules which either directly or indirectly depend on each other to function properly.
Such modules are also known as mutually recursive.

![link](https://4.bp.blogspot.com/-BruN-H9P0wo/VY_9LCisioI/AAAAAAAAAns/fmQSLOXTMBQ/s1600/Circular%2B%2BPackage%2BDependency.png)

**Fixing methods:**
 - **Add additional abstractions (Interfaces);**  
    - Before:  
      ![link](https://i.stack.imgur.com/A1fRz.png)
      
    - After:  
      ![link](https://i.stack.imgur.com/MUzQk.png)
      
 - **Broke dependency chain;**
 - **Chain modules can be combined into a single module;**