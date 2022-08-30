# Garbage collector

**The JS garbage collection** is the process that’s responsible for clearing out unused objects from memory.
While this is a necessary and good process, and it is highly optimized (and keeps being optimized all the
time), it has performance implications. The process runs on the main thread, and hence has the potential,
in some cases, to block the JavaScript Event Loop.

**JS memory model:**
- **Root object:**
  - Локальные переменные и параметры текущей функции.
  - Переменные и параметры других функций в текущей цепочке вложенных вызовов.
  - Глобальные переменные.
  - (некоторые другие внутренние значения)
- **Linked objects:**

## <ins>Reachability concept:</ins>
![link](https://drive.google.com/uc?id=1nUimAH_1-isjbHxnRNrAbvPvW7KRHHLq)  
- **One link:**  
  **<ins>Example:</ins>**
  ```js
  let user = {
    name: "John"
  };
  ```
  ![link](https://drive.google.com/uc?id=16X1C9YHWnCiYmho-59AAiE3VI5hVL7jv)  

  **<ins>GC processing:</ins>**
  ```js
  user = null;
  ```
  ![link](https://drive.google.com/uc?id=1TXJq-t6qMoc5ZzELB2jhdULfx-zjZedZ)  

- **Two links:**  
  **<ins>Example:</ins>**
  ```js
  let user = {
    name: "John"
  };
  
  let admin = user;
  ```
  ![link](https://drive.google.com/uc?id=1NEOYZSVdMfuWWoxNQrFTx7b6BvVAPhtI)  

  **<ins>GC processing:</ins>**
   ```js
  user = null;
  ```
  Oбъект John всё ещё достижим через глобальную переменную admin, поэтому он находится в памяти. Если бы мы
  также перезаписали admin, то John был бы удалён.

- **Intersected objects:**  
  **<ins>Example:</ins>**
  ```js
  function marry(man, woman) {
    woman.husband = man;
    man.wife = woman;
  
    return {
      father: man,
      mother: woman
    }
  }
  
  let family = marry({
      name: "John"
    }, {
      name: "Ann"
  });
  ```
  ![link](https://drive.google.com/uc?id=1o1YPHDHEPvBGlEoY_xQvgLy69UAqmZiM)  

  **<ins>GC processing:</ins>**
   ```js
  delete family.father;
  delete family.mother.husband;
  ```
  ![link](https://drive.google.com/uc?id=1f5Zfi22RpuOFycojAIwalEkhLy6GvCiS)  
  Исходящие ссылки не имеют значения. Только входящие ссылки могут сделать объект достижимым. Объект John
  теперь недостижим и будет удалён из памяти со всеми своими данными, которые также стали недоступны.

- **Unreachable island:**  
  **<ins>Example:</ins>**
  ```js
  function marry(man, woman) {
    woman.husband = man;
    man.wife = woman;

    return {
      father: man,
      mother: woman
    }
  }
  
  let family = marry({
      name: "John"
    }, {
      name: "Ann"
  });
  ```
  ![link](https://drive.google.com/uc?id=1o1YPHDHEPvBGlEoY_xQvgLy69UAqmZiM)  

  **<ins>GC processing:</ins>**
   ```js
  family = null;
  ```
  ![link](https://drive.google.com/uc?id=1tH4rvaa4KEbuvU27MUSmISJaA8c82f6n)  
  Этот пример демонстрирует, насколько важна концепция достижимости. Объекты John и Ann всё ещё связаны, оба
  имеют входящие ссылки, но этого недостаточно. У объекта family больше нет ссылки от корня (stack memory), поэтому весь
  «остров» становится недостижимым и будет удалён.

## <ins>GC algorithms:</ins>
### 1) No-op collector (Eden memory allocation):
GC заботится только об аллокации новой памяти, а на умные стратегии сборки мусора можно забить.
Как только доступная куча заканчивается, начинается процедура остановки сервера.
**<ins>Memory allocation (fragmentation):</ins>**
  1) **Memory overfilling:**  
     ![link](https://habrastorage.org/r/w1560/webt/rg/ly/oy/rglyoyk5kjjz0re9ktp1m7r0dtg.png)  
     
  2) **No GC everything stops:**  
    ![link](https://habrastorage.org/r/w1560/webt/un/lw/gn/unlwgnwcw1-7p5xunjhvo2hfwzg.png)  

**<ins>Conclusion:</ins>**  
Для фронтенда no-op collector неактуален, но на бэкенде используется. Например, имея несколько 
серверов за балансировщиками, приложению отдается 32 Гб оперативки и потом оно убивается целиком.
Так проще и производительность только повышается за счет простого перезапуска, когда памяти
становится мало.
- **Pros:**
  - Сборщик очень простой.
  - Сборки мусора просто нет.
  - Не надо ничего писать и думать о памяти.
- **Cons:**
  - Все падает так, что больше никогда не поднимется;
  
### 2) Mark-and-sweep:
Основной алгоритм сборки мусора – **«алгоритм пометок» (англ. «mark-and-sweep»).**  
**Согласно этому алгоритму, сборщик мусора регулярно выполняет следующие шаги:**
  - Сборщик мусора «помечает» (запоминает) все корневые объекты.
  - Затем он идёт по их ссылкам и помечает все найденные объекты.
  - Затем он идёт по ссылкам помеченных объектов и помечает объекты, на которые есть ссылка от них. Все
    объекты запоминаются, чтобы в будущем не посещать один и тот же объект дважды.
  - …И так далее, пока не будут посещены все ссылки (достижимые от корней).
  - Все непомеченные объекты удаляются.
  
**<ins>Example:</ins>**  
![link](https://drive.google.com/uc?id=1PSt9c4FKDTixjLHH4JXtHqv76tkXt5PM)  

![link](https://drive.google.com/uc?id=1sWCHJlJGckbxwCVLlF9kufxg53P53ZcN)  

**<ins>Memory allocation (fragmentation):</ins>**  
  1) **Memory overfilling:**  
     ![link](https://habrastorage.org/r/w1560/webt/rg/ly/oy/rglyoyk5kjjz0re9ktp1m7r0dtg.png)  
  2) **Memory after GC (fragmentation):**  
     **Фрагментация памяти** — это когда большая часть вашей памяти выделяется в большом количестве
     несмежных блоков или блоков — оставляя значительный процент вашей общей памяти 
     нераспределенной, но непригодной для большинства типичных сценариев. Это приводит к 
     исключениям нехватки памяти или ошибкам выделения.
     ![link](https://drive.google.com/uc?id=1FpbOW9OmaqOgwW2yVLDCvSgWPEiyQOuE)  
     
**<ins>Conclusion:</ins>**
  - **Pros:**  
    - Очень простой алгоритм. Один из первых, про который вы узнаете, если начнете изучать Garbage
      collector.
    - Работает пропорционально количеству мусора, но справляется только, когда мусора мало.
    - Если у вас только живые объекты, то он не тратит время и просто ничего не делает.
  - **Cons:**  
    - Требует сложной логики поиска свободного места, потому что когда в памяти много дырок, то в 
      каждую приходится примерять объект, чтобы понять — подходит он или нет.
    - Фрагментирует память. Может произойти ситуация, что при свободных 200 Мб память разбита на 
      маленькие кусочки и, как в примере выше, нет цельного куска памяти под объект.
      
### 3) Mark-and-compact:
Принцип работы **«mark-sweep-compact»** похож на описанный выше «Mark-and-sweep», но добавляется
процедура «уплотнения» (defragmentation), позволяющая более эффективно использовать память. В процедуре живые 
объекты перемещаются в начало. Таким образом, мусор остается в конце памяти.

**<ins>Memory allocation (fragmentation):</ins>**
  1) **Memory overfilling:**   
   ![link](https://habrastorage.org/r/w1560/webt/rg/ly/oy/rglyoyk5kjjz0re9ktp1m7r0dtg.png)  
  2) **Memory after GC (defragmentation):**  
     **Дефрагментация (уплотнение) памяти** - объединение свободных блоков, перемещение программ в начало памяти и
     объединение свободных областей. На время уплотнения вычисления приостанавливаются.
     ![link](https://drive.google.com/uc?id=1UchRyM7lpTodwq8pPZG-pz6816YNAAs8)  

**<ins>Conclusion:</ins>**
  - **Pros:**  
    - Дефрагментирует память.
    - Работает пропорционально количеству живых объектов, а значит, можно использовать, когда
      мусора практически нет.
  - **Cons:**  
    - Сложный в работе и реализации.
    - Перемещает объекты. Мы подвинули объект, скопировали, теперь он находится в другом месте 
      и вся эта операция довольно дорогая.
    - Требует 2-3 прохода по всей памяти, в зависимости от реализации — алгоритм медленный.

### 4) Semi-space (Lisp 2):
**Semi-space garbage collection** is a copying algorithm, which means that reachable
objects are relocated from one address to another during a collection.
Available memory is divided into two equal-size regions called “old-space” and “new-space”.

**<ins>Memory allocation (fragmentation):</ins>**
  1) **Memory overfilling:**  
     ![link](https://drive.google.com/uc?id=1NCWoMOseuObwrGXSW1FA2DThMPQ4HIlj)  
  2) **Computing GC (starting relocation defragmentation):**  
     ![link](https://drive.google.com/uc?id=1Stcz7xuZaauu1-1wLZCqmKqrOgE_EVPW)  
  2) **Memory after GC (relocation defragmentation completed):**  
     ![link](https://drive.google.com/uc?id=1R_iBCJIOSskZRiRrhTG66uLuv1UH2ugW)  
     
**<ins>Conclusion:</ins>**
  - **Pros:**
    - Дефрагментирует память.
    - Простой.
    - Можно совместить с фазой обхода.
    - Работает пропорционально количеству живых объектов по времени.
    - Хорошо работает, когда много мусора. Если у вас есть 2 Гб памяти и в ней 3 объекта, то вы
      обойдете только 3 объекта, а остальных 2 Гб будто и не было.
  - **Cons:**
    - Двойной расход памяти. Вы используете памяти в 2 раза больше, чем надо.
    - Перемещает объекты — это тоже не очень дешевая операция.

### CONCLUSION:  
![link](https://habrastorage.org/r/w1560/webt/s9/zm/ec/s9zmecoite95yruxuvtafbzaimy.png)  

## <ins>V8 GC processing (generation collecting):</ins>
### Heap:
  - **Eden Space** (new space) — в этой области выделяется память под все создаваемые программой объекты.
    Жизненный цикл большей части объектов, к которым относятся итераторы, объекты внутри методов
    и т.п., недолгий.
  - **Survivor Space** (old space) — здесь хранятся перемещенные из Eden Space объекты после первой сборки 
    мусора. Объекты, пережившие несколько сборок мусора, перемещаются в следующую сборку Tenured
    Generation.
  - **Tenured Generation** (large object space) — хранит долгоживущие объекты. Когда данная область памяти заполняется,
    выполняется полная сборка мусора (full, major collection).
    
![link](https://i.imgur.com/kSgatSL.png)

### Generation collecting (single-thread):
  1) Создается объект в Eden. 
  2) В какой-то момент в Eden становится слишком много мусора и объект перекладывается в 
     Semispace.  
  3) Объект подростает и когда сборщик понимает, что он слишком старый и скучный, то 
     перекидывает в Mark and Sweep, в котором сборка мусора производится крайне редко.
   
**Algorithms Generation collecting:**  
![link](https://habrastorage.org/r/w1560/webt/u-/-7/r4/u--7r4ggek0kxgpscwhtzn8grfe.png)

**Heap memory allocation Generation collecting:**  
![link](https://v8.dev/_img/orinoco-parallel-scavenger/cheneys-semispace-copy.png)

**Single thread Generation collecting:**  
![link](https://v8.dev/_img/orinoco-parallel-scavenger/cheneys-semispace-copy-processing.png)  
![link](https://javascriptperformance.dev/wp-content/uploads/2021/02/image-1536x272.png)

## <ins>GC optimizations:</ins>
### 1) <ins>Algorithms:</ins>
  - ### Trick GC: 
    Полагаясь на гипотезу поколений, мы решили, что объекты с, g, i скорее всего проживут еще 
    долго, и можно проверять их на мусор реже. Зная эту гипотезу, можно писать программы, которые
    обманывают сборщик. **Так можно делать, но я вам не советую, потому что это приведет почти 
    всегда к нежелательным эффектам.** Если создавать долгоживущий мусор, сборщик начнет считать, 
    что его не требуется собирать.  
    __  
    **Классический пример обмана — LRU-cache.** В кэше долго лежит объект, сборщик смотрит на него
    и считает, что пока собирать не будет, потому что объект проживет еще очень долго. Потом в кэш
    попадает новый объект, а большой старый из него выталкивается и собрать этот большой объект 
    сразу уже нельзя.
    
    ![link](http://www.topjavatutorial.com/wp-content/uploads/2016/04/LRU-Cache.png)  
    
  - ### WeakRef:  
    A WeakRef object lets you hold a weak reference to another object, without preventing that
    object from getting garbage-collected.  
    **Объект WeakRef** содержит слабую ссылку на объект, который называется его целью или 
    референтом. Слабая ссылка на объект - это ссылка, которая не препятствует удалению объекта
    сборщиком мусора. Напротив, обычная (или сильная) ссылка сохраняет объект в памяти. Когда 
    объект больше не имеет сильных ссылок на него, сборщик мусора движка JavaScript может 
    уничтожить объект и освободить его память. Если это произойдет, вы больше не сможете получить
    объект из слабой ссылки.
  - ### Pool pattern:
    **Link:** https://github.com/21Michael/JS-arch-learning/blob/main/JavaScript/3)GOF-Design-Patterns/Creational/pool.js
  - ### Unsubscribe from events (removeEventListener());
  - ### Immutable objects:
    **Immutable objects** can be quite beneficial to optimizing GarbageCollected code. Because an 
    ImmutableObject cannot be modified, there are many garantees which can be made. 
      - **Pros (increase speed):** For example, you can't have circular references, and you don't have to worry about 
        modification under the GC's nose so it's easier to just use a **mark-and-sweep** based 
        GC. **Because every time when you run mark-and-sweep GC under the mutated object the 
        algorithm has to re-update all marks tree.**  
        ![link](https://drive.google.com/uc?id=11vXZ5MOeRNf4lIWO0Ifa-jL9JEBhyUxA)
        
      - **Cons (overflowing eden memory and triggers GC):** also, one of downsides of Immutable objects is that it can fast overfill your heap memory
        (create immutable objects in the loop), and overfilling of the heap is one of things that
        triggers GC running;
    
### 2) Threads computation:

  - ### Parallel:  
    В современных компьютерах не один поток выполнения. В вебе это знакомо по Web Workers. 
    Почему-бы не взять и не распараллелить процесс сборки. Произвести несколько маленьких
    операций одновременно будет быстрее, чем одну большую.    
    
    **Heap memory allocation Generation collecting:**  
    ![link](https://v8.dev/_img/orinoco-parallel-scavenger/parallel-scavenge.png)  
    
    **Multi threads Generation collecting:**  
    ![link](https://v8.dev/_img/orinoco-parallel-scavenger/parallel-scavenge-processing.png)      
    ![link](https://javascriptperformance.dev/wp-content/uploads/2021/02/image-1-1536x925.png)  
    
  - ### Incremental:  
    Incremental optimizations are focused on chunking the GC to small bits. This allows constant
    memory cleanup while keeping the GC chunks very short.  
    __  
    **Heap memory allocation Generation collecting:**  
    ![link](https://v8.dev/_img/orinoco-parallel-scavenger/parallel-scavenge.png)  

    **Multi threads Generation collecting:**  
    ![link](https://v8.dev/_img/orinoco-parallel-scavenger/parallel-scavenge-processing.png)     
    ![link](https://javascriptperformance.dev/wp-content/uploads/2021/02/image-2-1536x1267.png)  
    
  - ### Concurrent:
    Аккуратно сделать слепок текущего состояния, а сборку вести параллельно выполнению JS.  
    Optimizations that revolve around running some of the Garbage Collection algorithm along the 
    JavaScript code running in the main thread. We cannot really clear the memory while JavaScript
    is running, but we can start marking objects for removal.  
    __   
    **Multi threads Generation collecting:**  
    ![link](https://habrastorage.org/r/w1560/webt/lm/fd/3w/lmfd3w2kiyhtxlwvp1wtlges6ia.png)
