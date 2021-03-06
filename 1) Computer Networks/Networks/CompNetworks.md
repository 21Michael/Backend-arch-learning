# Computer Networks

## 1) Networks classification:
  - **Тип коммутации:**
    - `коммутация каналов (телефонные сети):` перед отправкой данных необходимо установить соединение "путь" 
      отправитель - получатель, по которому в дальнейшем будет происходить обмен данными;
    - `коммутация пакетов (компьютерные сети):` перед отправкой данные разделаются на пакеты которые проходят
      через сеть различными путями что делает их более отказо-устойчивыми но требует вычислений маршрутизации
      на каждом узле сети для выбора следующего узла;
  - **Технология передачи:**
    - `широковещательные сети (Ethernet, Wi-Fi):` данные передающиеся в сети доступны всем узлам;
    - `точка-точка (Ethernet)`: данные доступны только отправителю и получателю;
  - **Протяженность:**
    - `персональные (1м);`
    - `локальные (10м - 1км);`
    - `муниципальные (10км);`
    - `глобальные (100 - 1000км);`
    - `мировые (10 000км);`
    
###Link: https://youtu.be/Y4LK1OZ54h0?list=PLtPJ9lKvJ4oiNMvYbOzCmWy6cRzYAh9B1&t=99

## 2) Networks topology:  

**Топология** - способ объединение компьютеров между собой в сеть (граф). Граф где вершины являются узлами сети
(комп устройства, сервера, сетевое оборуд...) а ребра связями между ними.
- **Наиболее популярные графы:**
    - `полносвязная`: каждое устройство имеет соединение со всеми другими устройствами (прямые каналы).
    - `звезда`: передача происходит через центральное устройство (сетевое оборуд).
    - `кольцо`: передача данных по кольцу.
    - `дерево`
    - `шина`
    
![link](https://intuit.ru/EDI/25_07_20_1/1595629193-15985/tutorial/882/objects/4/files/04_16.jpg)

###Link: https://www.youtube.com/watch?v=z8VmkYahV8M&list=PLtPJ9lKvJ4oiNMvYbOzCmWy6cRzYAh9B1&index=3&ab_channel=AndreySozykin

## 3) Network elements:  

![link](https://drive.google.com/uc?id=17Fy8KosubLvkyEKHhxUx6fGNzxn3DXVX)

**Архитектура сети** - набор уровней и протоколов сети.  

![link](https://www.researchgate.net/profile/Wei-Sun-11/publication/332632662/figure/fig1/AS:751501697904642@1556183375621/Internet-Protocol-Stack.png)

**Стек протоколов** - это иерархически организованный набор сетевых протоколов, достаточный для организации 
взаимодействия узлов в сети. Протоколы работают в сети одновременно, значит работа протоколов должна быть 
организована так, чтобы не возникало конфликтов или незавершённых операций. Поэтому стек протоколов разбивается
на иерархически построенные уровни, каждый из которых выполняет конкретную задачу — подготовку, приём, передачу
данных и последующие действия с ними.  

**Стандартные стеки:**
  - **ISO** - это концептуальная модель, которая характеризует и стандартизирует то, как различные компоненты
    программных обеспечений и аппаратных средств, участвующие в сетевой коммуникации, должны разделять труд и
    взаимодействовать друг с другом:
    - **Уровень 1: прикладной уровень**  
      Прикладной уровень модели OSI напрямую взаимодействует с применениями программных обеспечений для 
      предоставления необходимых функций связи, и он наиболее близок к конечным пользователям. Функции 
      прикладного уровня обычно включают в себя проверку доступности коммуникационных партнеров и ресурсов
      для поддержки любой передачи данных. Этот уровень также определяет протоколы для конечных применений,
      такие как domain name system (DNS), file transfer protocol (FTP), hypertext transfer protocol (HTTP),
      Internet message access protocol (IMAP), post office protocol (POP), simple mail transfer protocol 
      (SMTP), Simple Network Management Protocol (SNMP), и Telnet (a terminal emulation).

    - **Уровень 2: уровень представления**  
      Уровень представления проверяет данные, чтобы обеспечить его совместимость с коммуникационными 
      ресурсами. Он переводит данные в форму, что прикладной уровень и более низкие уровни принимают.
      Уровень представления обеспечивает преобразование протоколов и кодирование/декодирование данных. 
      Запросы приложений, полученные с прикладного уровня, на уровне представления преобразуются в формат 
      для передачи по сети, а полученные из сети данные преобразуются в формат приложений. На этом уровне 
      может осуществляться сжатие/распаковка или шифрование/дешифрование, а также перенаправление запросов
      другому сетевому ресурсу, если они не могут быть обработаны локально.

    - **Уровень 3: сеансовый уровень**  
      Сеансовый уровень управляет диалогами (соединениями) между компьютерами. Он устанавливает, управляет, 
      сохраняет и в конечном итоге разрывает соединения между локальным и удаленным приложением. Программное 
      обеспечение уровня 5 также выполняет функции аутентификации и авторизации. Он проверяет, что данные 
      также доставляются. Сеансовый уровень обычно реализуется явно в прикладных средах, которые используют
      удаленные вызовы процедур.

    - **Уровень 4: транспортный уровень**  
      Транспортный уровень обеспечивает функции и средства передачи последовательностей данных от источника 
      к хосту назначения через одну или несколько сетей, сохраняя при этом функции quality of service (QoS) 
      и обеспечивая полную доставку данных. Целостность данных может быть гарантирована через исправление
      ошибок и аналогичные функции. Он также может предоставить явную функцию управления потоком. Хотя 
      протоколы TCP и User Datagram Protocol (UDP) не строго соответствуют модели OSI, они являются важными
      протоколами на уровне 4.

    - **Уровень 5: сетевой уровень**  
      Сетевой уровень обрабатывает маршрутизацию пакетов через логическую адресацию и функции коммутации. 
      Сеть - это среда, к которой можно подключить множество узлов. У каждого узла есть адрес. Когда узел 
      должен передать сообщение другим узлам, он может просто предоставить содержание СМС и адреса узла 
      назначения, затем сеть найдет способ доставки сообщения узлу назначения, возможно через другие узлы.
      Если сообщение слишком длинное, сеть может разделить его на несколько сегментов на одном узле, отправив
      их отдельно и повторно собрав фрагменты на другом узле.

    - **Уровень 6: канальный уровень**  
      Канальный уровень предназначен для обеспечения взаимодействия сетей на физическом уровне и контроля
      ошибок, которые могут возникнуть. Полученные с физического уровня данные, представленные в битах, он
      упаковывает в кадры, проверяет их на целостность и, если нужно, исправляет ошибки (формирует повторный
      запрос повреждённого кадра) и отправляет на сетевой уровень. Канальный уровень обычно делится на два
      подуровня - уровень media access control (MAC) layer и logical link control (LLC) . Уровень MAC 
      отвечает за управление тем, как устройства в сети получают доступ к мультимедиа и разрешение на 
      передачу данных. Уровень LLC отвечает за идентификацию и инкапсуляцию протоколов сетевого уровня, а 
      также контролирует проверку ошибок и синхронизацию кадров.

    - **Уровень 7: физический уровень**  
      Физический уровень определяет электрические и физические характеристики соединения данных. Например, 
      расположение штырей разъема, рабочие напряжения электрического кабеля, спецификации оптоволоконного 
      кабеля и частота для беспроводных устройств. Он отвечает за передачу и прием неструктурированных 
      необработанных данных в физической среде. Управление скоростью передачи битов осуществляется на 
      физическом уровне. Это уровень сетевого оборудования низкого уровня и никогда не касается протоколов
      или других элементов более высокого уровня.

![link](https://cf.ppt-online.org/files/slide/o/oM5dKjFOqrwp9f0DXz4gCTy6JBZsNbA8lUSL1n/slide-2.jpg)
    
  - **TCP/IP** - также является многоуровневой сетевой моделью, но это четырехуровневая модель. Он широко 
    известен как TCP/IP, поскольку основными протоколами являются TCP и IP, но в этой модели используются 
    не только эти два протокола:  
    
    **1. Прикладной уровень**  
    На прикладном уровне (Application layer) работает большинство сетевых приложений. Эти программы имеют 
    свои собственные протоколы обмена информацией, например, HTTP для WWW, FTP (передача файлов), SMTP 
    (электронная почта), SSH (безопасное соединение с удалённой машиной), DNS (преобразование символьных 
    имён в IP-адреса) и многие другие.

    **2. Транспортный уровень**  
    Транспортный уровень, также известный как транспортный уровень хост-хост, отвечает за предоставление 
    прикладного уровня сервисами связи сеанса и датаграмм. Основными протоколами этого уровня являются TCP 
    и UDP. Протокол TCP обеспечивает один-на-один, ориентированную на соединение, надежную службу связи. 
    Он отвечает за последовательность и подтверждение отправленных пакетов, а также восстановление пакетов,
    потерянных при передаче. UDP предоставляет один-к-одному или один-ко-многим, без подключения, ненадежную
    службу связи. UDP обычно используется, когда объем передаваемых данных невелик (например, данные 
    помещаются в один пакет).

    **3. Сетевой уровень**  
    Сетевой уровень отвечает за адресацию хостов, упаковку и функции маршрутизации. Основными протоколами 
    сетевого уровня являются IP, протокол разрешения адресов (ARP), протокол управляющих сообщений Интернета
    (ICMP) и протокол управления группами Интернета (IGMP). IP - это маршрутизируемый протокол, отвечающий 
    за IP-адресацию, маршрутизацию и фрагментацию и повторную сборку пакетов. ARP отвечает за обнаружение 
    адреса уровня сетевого доступа, такого как адрес аппаратных средств, связанный с данным доступом к 
    Интернет-уровню. ICMP отвечает за предоставление диагностических функций и отчетов об ошибках из-за 
    неудачной доставки IP-пакетов. IGMP отвечает за управление многоадресными группами IP. На этом уровне 
    IP добавляет заголовок к пакетам, который известен как IP-адрес. Сейчас есть IPv4 (32-битный) адрес и
    IPv6 (128-битный) адрес.
    
    **4. Канальный уровень**  
    Канальный уровень (Link layer) описывает, каким образом передаются пакеты данных через физический 
    уровень, включая кодирование (то есть специальные последовательности бит, определяющих начало и конец 
    пакета данных). Канальный уровень иногда разделяют на 2 подуровня — LLC и MAC. Кроме того, канальный 
    уровень описывает среду передачи данных (будь то коаксиальный кабель, витая пара, оптическое волокно 
    или радиоканал), физические характеристики такой среды и принцип передачи данных (разделение каналов,
    модуляцию, амплитуду сигналов, частоту сигналов, способ синхронизации передачи, время ожидания ответа и
    максимальное расстояние).
    
![link](https://bstudy.net/htm/img/4/14659/119.png)

**Сетевая модель:**

![link](https://drive.google.com/uc?id=19NuhzTKPn7iPH5FLEHopzxiMmIm60zg6)