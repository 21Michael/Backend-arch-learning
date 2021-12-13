# Dependency injection / Inversion of control principle

## <ins>Inversion of control principle:
This states that a class should not configure its dependencies statically but should be
configured by some other class from outside.

It is the fifth principle of **S.O.L.I.D** — the five basic principles of object-oriented
programming and design by Uncle Bob — which states that a class should depend on 
abstraction and not upon concretions (in simple terms, hard-coded).

![link](https://trile.dev/diagram/ioc.svg)

## <ins>DI:
**DI** is a pattern where, instead of creating or requiring dependencies directly
inside a module (**HIDDEN STATE**), we pass them as parameters or reference.

![link](https://miro.medium.com/max/741/1*VPKY-RbVhLZierPrCwRiKQ.png)

### HIDDEN STATE Examples:
   ```js
    const usersRepository = require('./...'); // direct module dependencies !!!!!!!!!!!!
    const mailer = require('./...'); // direct module dependencies !!!!!!!!!!!!
    const logger = require('./...'); // direct module dependencies !!!!!!!!!!!!
    
    class UsersService {
      constructor() {
        this.usersRepository = usersRepository; // hidden state properties !!!!!!!!!!!!!
        this.mailer = mailer; // hidden state properties !!!!!!!!!!!!!
        this.logger = logger; // hidden state properties !!!!!!!!!!!!!
      }
      
      async findAll() {
        return this.usersRepository.findAll();
      }
      
      async addUser(user) {
        await this.usersRepository.addUser(user);
        this.logger.info(`User created: ${user}`);
        await this.mailer.sendConfirmationLink(user);
        this.logger.info(`Confirmation link sent: ${user}`);
      }
    }
    
    module.exports = UsersService;
    
    const usersService = new UsersService(); // unpredictable code !!!!!!!!!!!!!!!!
   ```

### DI Examples:
  1) **OOP:**
     ```js
      class UsersService {
        constructor({ usersRepository, mailer, logger }) {
          this.usersRepository = usersRepository; // injected constructer properties !!!!!!!!!!!!!
          this.mailer = mailer; // injected constructer properties !!!!!!!!!!!!!
          this.logger = logger; // injected constructer properties !!!!!!!!!!!!!
        }
        
        async findAll() {
          return this.usersRepository.findAll();
        }
        
        async addUser(user) {
          await this.usersRepository.addUser(user);
          this.logger.info(`User created: ${user}`);
          await this.mailer.sendConfirmationLink(user);
          this.logger.info(`Confirmation link sent: ${user}`);
        }
      }
      
      module.exports = UsersService;
      
      const usersService = new UsersService({
        usersRepository,
        mailer,
        logger
      }); // injecting outside dependencies !!!!!!!!!!!!!!!!
     ```
  2) **Functional:**
     ```js
      export const usersService = ({ usersRepository, mailer, logger }) => { // injected function parameters !!!!!!!!!!!!!
        const findAll = () => dependencies.usersRepository.findAll();
        const addUser = user => {
          await dependencies.usersRepository.addUser(user)
          dependencies.logger.info(`User created: ${user}`)
          await dependencies.mailer.sendConfirmationLink(user)
          dependencies.logger.info(`Confirmation link sent: ${user}`)
        };
      
        return {
          findAll,
          addUser
        };
      }
      
      const service = usersService({
        usersRepository,
        mailer,
        logger
      }); // injecting outside dependencies !!!!!!!!!!!!!!!!
     ```

## Benefits of using DI:
  - **Helps in Unit testing.**
  - **Boiler plate code is reduced, as initializing of dependencies is done by the
    injector component.**
  - **Extending the application becomes easier.**
  - **Helps to enable loose coupling, which is important in application programming.**