# RPC (Remote Procedure Call)

**Удаленный вызов процедур (RPC)** — это метод межпроцессного взаимодействия. Используется для 
клиент-серверных приложений. Механизмы RPC используются, когда компьютерная программа вызывает 
выполнение процедуры или подпрограммы в другом адресном пространстве, которое закодировано как 
обычный вызов процедуры, при этом программист специально не кодирует детали для удаленного 
взаимодействия.

There is a method and some arguments, and that is pretty much it. Think of it like calling a 
function in JavaScript, taking a method name and arguments. 

**RPC call example:**
```
    POST /sayHello HTTP/1.1
    HOST: api.example.com
    Content-Type: application/json
    
    {"name": "Racey McRacerson"}
```
 JS analogy:
```js
    /* Signature */
    function sayHello(name) {
      // ...
    }
    
    /* Usage */
    sayHello("Racey McRacerson");
```


**Типы RPC:**
  - **Обратный вызов RPC;**  
    Этот тип RPC обеспечивает парадигму P2P между участвующими процессами. Это помогает процессу быть как 
    клиентом, так и сервером.
  - **Трансляция RPC;**  
    Широковещательный RPC — это запрос клиента, который транслируется в сети и обрабатывается всеми 
    серверами, у которых есть метод обработки этого запроса.
  - **RPC в пакетном режиме;**  
    RPC в пакетном режиме помогает ставить в очередь отдельные запросы RPC в буфере передачи на стороне
    клиента, а затем отправлять их по сети одним пакетом на сервер.

### Схема работы RPC
**Архитектура RPC имеет в основном пять компонентов программы:**
  - **клиент**
  - **Клиентская заглушка**  
    On the client side, the stub handles the interface between the client’s local procedure call
    and the run-time system, marshaling and unmarshaling data, invoking the RPC run-time protocol, 
    and if requested, carrying out some of the binding steps.
  - **RPC Runtime**  
    RPC run-time system is a library of routines and a set of services that handle the network 
    communications that underlie the RPC mechanism. In the course of an RPC call, client-side and 
    server-side run-time systems’ code handle binding, establish communications over an appropriate
    protocol, pass call data between the client and server, and handle communications errors.
  - **Серверная заглушка**  
    On the server side, the stub provides a similar interface between the run-time system and the local 
    manager procedures that are executed by the server.
  - **сервер**

A client invokes a remote procedure, serializes the parameters and additional information into a message,
and sends the message to a server. On receiving the message, the server deserializes its content, executes
the requested operation, and sends a result back to the client. The server stub and client stub take care 
of the serialization and deserialization of the parameters.

![link](https://coderlessons.com/wp-content/uploads/images/gur/8a0fd91187a467189a4a3c1662b1d11a.png)

**RPC uses two HTTP methods: GET, POST. Usually in API used one of these methods:**

![link](https://habrastorage.org/r/w1560/webt/m2/i2/ua/m2i2uadak8sdzbge_pvqlnpu55s.png)

### RPC Pros:
  - **Straightforward and simple interaction.**  
    RPC uses GET to fetch information and POST for everything else. The mechanics of the interaction 
    between a server and a client come down to calling an endpoint and getting a response.
  - **Easy-to-add functions.**   
    If we get a new requirement for our API, we can easily add another endpoint executing this 
    requirement: 1) Write a new function and throw it behind an endpoint and 2) now a client can hit 
    this endpoint and get the info meeting the set requirement.
  - **High performance.**   
    Lightweight payloads go easy on the network providing high performance, 
    which is important for shared servers and for parallel computations executing on networks of 
    workstations. RPC is able to optimize the network layer and make it very efficient with sending 
    tons of messages per day between different services.
    
### RPC Cons:
  - **Tight coupling to the underlying system.**  
    An API’s abstraction level contributes to its reusability. The tighter it is to the underlying system,
    the less reusable it will be for other systems. RPC’s tight coupling to the underlying system doesn’t 
    allow for an abstraction layer between the functions in the system and the external API. This raises 
    security issues as it’s quite easy to leak implementation details about the underlying system into 
    the API.
  - **Low discoverability.**   
    In RPC there’s no way to introspect the API or send a request and start understanding what function
    to call based on its requests.
  - **Function explosion.**   
    It’s so easy to create new functions. So, instead of editing the existing ones, we create new ones
    ending up with a huge list of overlapping functions that are hard to understand.

### RPC use cases:
The RPC pattern started being used around the 80s, but this doesn’t automatically make it obsolete. Big 
companies like Google, Facebook (Apache Thrift), and Twitch (Twirp) are using RPC high-performance variates
internally to perform extremely high-performance, low-overhead messaging. Their massive microservices
systems require internal communication to be clear while arranged in short messages.

##XML-RPC: 
**XML-RPC is a remote procedure call (RPC)** protocol which uses XML to encode its calls and HTTP as a 
transport mechanism.

##JSON-RPC:
**JSON-RPC** is a remote procedure call protocol encoded in JSON. It is similar to the XML-RPC protocol,
defining only a few data types and commands. JSON-RPC allows for notifications (data sent to the server 
that does not require a response) and for multiple calls to be sent to the server which may be answered 
asynchronously.

##gRPC:
**gRPC** is an open-source RPC architecture designed by Google to achieve high-speed communication 
between microservices. gRPC allows developers to integrate services programmed in different languages.
gRPC uses the Protobuf (protocol buffers) messaging format, which is a highly-packed, highly-efficient
messaging format for serializing structured data.

Как вариант архитектуры RPC, gRPC был создан Google для ускорения передачи данных между микросервисами 
и другими системами, которым необходимо взаимодействовать друг с другом. По сравнению с REST API, 
gRPC API уникальны в следующих отношениях:
 - **Протобуф (Protobuf) вместо JSON**
 - **Построен на HTTP 2 вместо HTTP 1.1**
 - **Создание собственного кода вместо использования сторонних инструментов, таких как Swagger**
 - **Передача сообщений в 7-10 раз быстрее**
 - **Более долгая имплементация и реализация, чем REST**



**Protocol Buffers (protobuf)**  
Protobuf формат сериализации используемый по умолчанию для передачи данных между клиентом и сервером. 
Используя строгую типизацию полей и бинарный формат для передачи структурированных данных потребляет 
меньше ресурсов. Время выполнения процесса сериализации/десериализации значительно меньше как и размер 
сообщений в отличии от JSON/XML.

Для написания protobuf файлов используют язык описания интерфейсов (IDL). Например,
чтобы описать структуру данных сообщения, нужно добавить message, имя структуры, а внутри тип, 
название и номер поля.

```
message Car {
  required string model = 1;

  enum BodyType {
    sedan = 0;
    hatchback = 1;
    SUV = 2;
  }

  required BodyType type = 2 [default = sedan];
  optional string color = 3;
  required int32 year = 4;

  message Owner {
    required string name = 1;
    required string lastName = 2; 
    required int64 driverLicense = 3;
  }

  repeated Owner previousOwner = 5;
}
```

**Когда использовать API gRPC**  

  - **Соединения с микросервисами:** связь с низкой задержкой и высокой пропускной способностью
    gRPC делает его особенно полезным для подключения архитектур, состоящих из легких микросервисов,
    где эффективность передачи сообщений имеет первостепенное значение.
    
![link](https://docs.microsoft.com/ru-ru/dotnet/architecture/cloud-native/media/grpc-implementation.png)

  - **Системы где используется несколько языков программирования:** 
    благодаря поддержке генерации собственного кода для широкого спектра языков разработки, gRPC 
    отлично подходит для управления соединениями в среде с наличием нескольких языков.
  - **Потоковая передача в реальном времени:** когда требуется связь в реальном времени, 
    способность gRPC управлять двунаправленной потоковой передачей позволяет вашей системе отправлять
    и получать сообщения в режиме реального времени, не дожидаясь ответа отдельного клиента.
  - **Сети с низким энергопотреблением и низкой пропускной способностью:** использование gRPC 
    сериализованных сообщений Protobuf обеспечивает легкий обмен сообщениями, большую эффективность 
    и скорость для сетей с ограниченным диапазоном пропускания и маломощных сетей (особенно по 
    сравнению с JSON). Интернет вещей может быть примером такой сети, в которой могут быть полезны 
    API gRPC.
    
![link](https://res.cloudinary.com/practicaldev/image/fetch/s--y0xibxgW--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/i/w2vs79qbx9i1re9zoiw2.png)