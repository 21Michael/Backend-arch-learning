# Message queue (async communication)

Асинхронное выполнение операций на платформе Node.js дает существенные преимущества.  
**Это касается и обмена сообщениями:**
  - параллельная обработка сообщений;
  - возможность их хранения неопределенное время с последующей доставкой позднее 
    (**message queue**);
    
**Очереди сообщений** - компоненты, которые являются посредниками между отправителем 
и получателем, хранящими сообщения, пока они не будут доставлены до места назначения.  
Если по какой-либо причине получатель завершит работу, отключится от сети или
окажется под высокой нагрузкой, сообщения будут накапливаться в очереди и переданы 
получателю, когда он вернется в сеть и восстановит свою работоспособность.  
Очередь может находиться внутри отправителя, охватывать отправителя и получателя или
быть помещена в выделенную внешнюю систему, действующую независимо, как промежуточное
программное обеспечение для организации связи.

![link](https://drive.google.com/uc?id=1tLI46wlrzX3ewmqgiuYgP7SxTmx3OhVC)

## Messaging architecture:

![link](https://drive.google.com/uc?id=1WXcV8Sv-pzBe4VHuJ9-SrkPswXt-w2Ya)

  - ### Broker-less messaging;
    In a brokerless architecture, services can exchange messages directly.  
    **ZeroMQ** is a popular brokerless messaging technology. It’s both a specification
    and a set of libraries for different languages. It supports a variety of transports,
    including TCP, UNIX-style domain sockets, and multicast.  
    **Pros:**
    - Allows lighter network traffic and better latency, because messages go directly
    from the sender to the receiver, instead of having to go from the sender to the
    message broker and from there to the receiver
    - Eliminates the possibility of the message broker being a performance bottle-
    neck or a single point of failure
    - Features less operational complexity, because there is no message broker to set
    up and maintain  
      
    **Cons:**  
    - Services need to know about each other’s locations and must therefore use one
    of the discovery mechanisms.
    - It offers reduced availability, because both the sender and receiver of a message
    must be available while the message is being exchanged.
    - Implementing mechanisms, such as guaranteed delivery, is more challenging.
      
  - ### Broker messaging (Event-driven architecture);
    A message broker is an intermediary through which all messages flow. A sender writes
    the message to the message broker, and the message broker delivers it to the receiver.
    An important benefit of using a message broker is that the sender doesn’t need to
    know the network location of the consumer. Another benefit is that a message broker
    buffers messages until the consumer is able to process them.  
    **<ins>Popular open source message brokers:</ins>** ActiveMQ, RabbitMQ, Apache Kafka, AWS SQS;  
    **<ins>Characteristics:</ins>**
    - **Supported programming languages** — You probably should pick one that supports a
    variety of programming languages.
    - **Supported messaging standards** — Does the message broker support any standards,
    such as AMQP and STOMP, or is it proprietary?
    - **Messaging ordering** — Does the message broker preserve ordering of messages?
    - **Delivery guarantees** — What kind of delivery guarantees does the broker make?
    - **Persistence** — Are messages persisted to disk and able to survive broker crashes?
    - **Durability** — If a consumer reconnects to the message broker, will it receive the
    messages that were sent while it was disconnected?
    - **Scalability** — How scalable is the message broker?
    - **Latency** — What is the end-to-end latency?
    - **Competing consumers** — Does the message broker support competing consumers?  
      
    **<ins>Each message broker implements the message channel concept in a different way:</ins>**
    ![link](https://drive.google.com/uc?id=1RRAZIWnzQ7LA5UIu3jQzzA6PONsX57ik)

    **Pros:**
    - **Loose coupling** — A client makes a request by simply sending a message to the
    appropriate channel. The client is completely unaware of the service instances.
    It doesn’t need to use a discovery mechanism to determine the location of a ser-
    vice instance.
    - **Message buffering** — The message broker buffers messages until they can be pro-
    cessed. With a synchronous request/response protocol such as HTTP, both the
    client and service must be available for the duration of the exchange. With mes-
    saging, though, messages will queue up until they can be processed by the con-
    sumer. This means, for example, that an online store can accept orders from
    customers even when the order-fulfillment system is slow or unavailable. The
    messages will simply queue up until they can be processed.
    - **Flexible communication** — Messaging supports all the interaction styles described
    earlier.
    - **Explicit interprocess communication** — RPC-based mechanism attempts to make invok-
    ing a remote service look the same as calling a local service. But due to the laws
    of physics and the possibility of partial failure, they’re in fact quite different.  
      
    **Cons:**
    - **Potential performance bottleneck** — There is a risk that the message broker could be
    a performance bottleneck. Fortunately, many modern message brokers are
    designed to be highly scalable.
    - **Potential single point of failure** — It’s essential that the message broker is highly
    available—otherwise, system reliability will be impacted. Fortunately, most mod-
    ern brokers have been designed to be highly available.
    - **Additional operational complexity** — The messaging system is yet another system
    component that must be installed, configured, and operated.
    
## Protocols:
  - ### Advanced Message Queuing Protocol (AMQP):
    **Протокол AMQP** – открытый стандартный протокол, поддерживаемый многими
    системами сообщений с очередями. Помимо общего коммуникационного протокола,
    он также определяет модель для описания маршрутизации, фильтрации, организации
    очередей, надежности и безопасности.
    
    ![link](https://drive.google.com/uc?id=1_pAUdfm8IG3dPUN49AixSSMi41jdtmV8)
    
    **В AMQP имеются три основных компонента:**
      - **Queue:** структура данных, отвечающая за хранение сообщений, извлекаемых
        получателями. Сообщения из очереди передаются одному или нескольким получателям, 
        которыми, по сути, являются наши приложения. Если к одной очереди подключится 
        несколько получателей, сообщения будут распределяться между ними.  
        __   
        **Очереди могут быть следующих видов:**
          - **Надежные:** очередь автоматически восстанавливается при перезапуске
            брокера. Надежность не означает, что будет сохранено все содержимое 
            очереди; на диск будут сохранены только сообщения, отмеченные как 
            хранимые, и они же будут восстановлены в случае перезагрузки;
          - **Эксклюзивные:** к очереди может быть подключен только один конкретный
            подписчик. После закрытия соединения очередь уничтожается;
          - **Автоматически удаляемые:** очередь удаляется после отключения последнего
            подписчика;
      - **Коммутатор:** Коммутатор направляет сообщения в одну или несколько очередей
        в зависимости от реализуемого алгоритма: 
          - **Прямое коммутирование:** выбор маршрута определяется путем сопоставления 
            полного ключа маршрутизации (например, chat.msg);
          - **Тематическое коммутирование:** выбор маршрута определяется путем 
            сопоставления ключа с шаблоном (например, chat.# соответствует всем 
            ключам маршрутизации, начинающимся с chat);
          - **Разветвляющее коммутирование:** сообщения рассылаются во все подключенные
            очереди, независимо от ключа маршрутизации.
      - **Связь:** между коммутаторами и очередями. Также определяет ключ 
        маршрутизации или шаблон для фильтрации сообщений, поступающих от коммутатора.    
    __   
    Эти компоненты управляются брокером, предоставляющим программный интерфейс для
    создания и управления ими:
    ![link](https://drive.google.com/uc?id=1ZYylhNDvPEEoiHJlb2S_alv9XF0uh1zR)
        
    - ### Message Queue Telemetry Transport (MQTT):
    - ### Simple/Streaming Text Orientated Messaging Protocol (STOMP) : 
    