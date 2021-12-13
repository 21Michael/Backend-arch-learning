# Modularity

**Modularity** can be defined as a mechanism where a complex system is divided into several
components that are referred to as ‘modules’. Now, whenever a customer requests to 
develop software we can use or integrate these modules to develop new software.

![link](https://www.ytechie.com/2008/06/i-finally-get-the-point-of-inversion-of-control/ioc-diagrams.gif)

## Usage of modularity conception:  
### 1. Architectural Design:
In the architectural design phase, the large-scale structure of the software is
determined. You have to be very careful while creating modularity at this phase as
you have to the entire logical structure of the software.  
**Example:** dividing to microservices, dividing on layers...

### 2. Components Design
If you have created modularity in the architectural design of the software it becomes
easy to figure out and design the individual components. The modular components have
a well-defined purpose and they have a few connections with the other components.

### 3. Debugging
If the components are designed using modularity then it becomes easy to track them 
down. You can easily debug which component is responsible for the error.
Now as we say that the components have little connection to other components of the 
software so correcting a single component will not have an adverse effect on the 
other component.

### 4. Testing
Once the components are integrated to develop software it becomes almost impossible 
to test the entire software at once. Testing one component at a time is much easier.

### 5. Maintenance
Maintenance is a process of fixing or enhancing the system, to perform according to 
users need. Here also modularity plays a vital role. As making changes to a module 
must not affect another connected module in the system.

### 6. Independent Development
Software is never developed by one person. There is a team of people who develop the
software in terms of modules and components. Each person in a team is assigned to 
develop an individual component that’s why they also have to take care that the 
interfaces between the components are few and all of them are clear.

### 7. Damage Control
If the connection between the components of the system is few and clear then the 
error in one component will not spread damage to the other components of the system.

### 8. Software Reuse
Good modularity makes you reuse the component of the earlier software.   
The reusable components must:
  - Provide some useful service.
  - It must perform a single function.
  - Have few and clear connections to other components in the systems.

## Сцепленность (cohesion) и связанность (coupling):
![link](https://programmerbay.com/wp-content/uploads/2020/05/cohesion-vs-coupling.png)

### Сцепленность (cohesion): 
мера корреляции функций компонента между собой.
Например, модуль, предназначенный для выполнения только одного действия,
когда все его элементы подчинены решению одной задачи, обладает высокой
сцепленностью. Модуль, содержащий функции для сохранения объектов любо­
го типа в базу данных, такие как saveProduct(), saveInvoice(), saveUser() и т. д.,
имеет низкую сцепленность;

### Связанность (coupling): 
мера зависимости от других компонентов системы.
Например, модуль тесно связан с другим модулем, если непосредственно чи­
тает или изменяет данные другого модуля. Кроме того, два модуля, взаимо­
действующих через глобальное или общее состояние, также тесно связаны.
С другой стороны, два модуля, взаимодействующих только через передачу па­
раметров, слабо связаны.

**Наиболее желательна высокая сцепленность при слабой связанности, что обеспечивает 
наглядность, возможность повторного использования и расширяемость модулей.**

![link](https://upload.wikimedia.org/wikipedia/commons/thumb/0/09/CouplingVsCohesion.svg/1024px-CouplingVsCohesion.svg.png)