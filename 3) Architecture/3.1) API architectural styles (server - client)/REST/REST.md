# REST (Representational state transfer)

**REpresentational State Transfer** — это архитектура, т.е. принципы построения распределенных 
гипермедиа систем, того что другими словами называется World Wide Web, включая универсальные 
способы обработки и передачи состояний ресурсов по HTTP

![link](https://content.altexsoft.com/media/2020/05/word-image-59.png)

Чтобы распределенная система считалась сконструированной по REST архитектуре (Restful), 
необходимо, чтобы она удовлетворяла следующим критериям.

## REST-ful principles:

###  1) Client-Server
Система должна быть разделена на клиентов и на серверов. Разделение интерфейсов означает, что, 
например, клиенты не связаны с хранением данных, которое остается внутри каждого сервера, так что 
мобильность кода клиента улучшается. Серверы не связаны с интерфейсом пользователя или состоянием,
так что серверы могут быть проще и масштабируемы. Серверы и клиенты могут быть заменяемы и 
разрабатываться независимо, пока интерфейс не изменяется.

###  2) Stateless
Сервер не должен хранить какой-либо информации о клиентах. В запросе должна храниться вся 
необходимая информация для обработки запроса и если необходимо, идентификации клиента.

###  3) Cache
Каждый ответ должен быть отмечен является ли он кэшируемым или нет, для предотвращения повторного
использования клиентами устаревших или некорректных данных в ответ на дальнейшие запросы.

###  4) Uniform Interface:
Единый интерфейс определяет интерфейс между клиентами и серверами. Это упрощает и отделяет
архитектуру, которая позволяет каждой части развиваться самостоятельно.

   - ### Identification of resources
     В REST ресурсом является все то, чему можно дать имя. Например,пользователь, изображение, 
     предмет (майка, голодная собака, текущая погода) и т.д. Каждый ресурс в REST должен быть 
     идентифицирован посредством стабильного идентификатора, который не меняется при изменении 
     состояния ресурса. Идентификатором в REST является URI.  
      
      - **URI ( Resource Identifier)** — унифицированный (единообразный) идентификатор ресурса. 
     URI — последовательность символов, идентифицирующая абстрактный или физический ресурс.
     ![link](https://wiki.merionet.ru/images/url-i-uri-v-chem-razlichie/2.png)
     
         **Составляющие:**
          - **URL (Uniform Resource Locator)** -  адрес ресурса в сети, определяет местонахождение и 
            способ обращения к нему.
            ![link](https://alekseev74.ru/files/upload/images/pav43fmi.jpg)
            
          - **URN (Unifrorm Resource Name)** - имя ресурса в сети, определяет только название ресурса,
            но не говорит как к нему подключиться. Смысл URN в том, что им единоразово и уникально
            именуется какая-либо сущность в рамках конкретного пространства имен (контекста), либо
            без пространства имен, в общем (что не желательно). Таким образом, URN способен 
            преодолеть недостаток URL связанный с возможным будущим изменением и перемещением 
            ссылок, однако, теперь для того, чтобы знать местонахождение URN ресурса необходимо 
            обращаться к системе разрешения имен URN, в которой он должен быть зарегистрирован.
            ![link](https://alekseev74.ru/files/upload/images/ays1oq5k.jpg)
            
          - **URL + URN** 
     
   - ### Manipulation of resources through representations
     Представление в REST используется для выполнения действий над ресурсами. Представление 
     ресурса представляет собой текущее или желаемое состояние ресурса. Например, если ресурсом
     является пользователь, то представлением может являться XML или HTML описание этого 
     пользователя.
     
   - ### Self-descriptive messages
     Под само-описательностью имеется ввиду, что запрос и ответ должны хранить в себе всю 
     необходимую информацию для их обработки. Не должны быть дополнительные сообщения или кэши 
     для обработки одного запроса. Другими словами отсутствие состояния, сохраняемого между 
     запросами к ресурсам. Это очень важно для масштабирования системы.
     
   - ### HATEOAS (hypermedia as the engine of application state)
     In fact, some services are RESTful only to a degree. They have RPC style at the core, break
     down larger services into resources, and use HTTP infrastructure efficiently. But the key 
     part is using hypermedia aka HATEOAS.  
     --   
     **Hypermedia As The Engine Of Application State** – is one of the constraints of the REST 
     architecture. It means that with each response, a REST API provides metadata linking to all
     the related info about how to use the API. That’s what enables decoupling the client and the
     server. As a result, both API provider and API consumer can evolve independently without 
     hindering their communication. Neither REST nor HATEOAS is any requirement or specification.
     How you implement it depends only on you.
     
     ![link](https://grapeup.com/wp-content/uploads/2020/10/GrapeUp_Hateos_Graphics-3.jpg)

     Most projects these days are written using level 2. **<ins>They are actually using HTTP RPC.</ins>**
     If we would like to go for the perfect RESTful API, we should consider HATEOAS.  
     --  
     For adding metadata to our response used  special language: **HAL — язык гипертекстовых 
     приложений. Это формат, который обеспечивает простой и согласованный способ гиперссылки 
     между ресурсами в вашем REST API**  
     --  
     **С HAL у вас есть несколько категорий представлений:**

      - **Links (Ссылки):** комбинация (URI) ссылок на всевозможные связанные действий с данными 
        непосредственно связанными с полученными в ответе. Мы сами создаем и решаем какие ссылки
        надо добавлять.
        ```js
          {
            "id": 42,
            "first_name": "Adrien",
            "last_name": "Brault",
            "_links": {
              "self": {
                "href": "/api/users/42"
              },
              "users_amount": {
                "href": "/api/users/amount" // !!!!!!!!!!!!!!!!!!!!!!!!
              },
              "user_last": {
                "href": "/api/users/last" // !!!!!!!!!!!!!!!!!!!!!!!!
              },
              "users": {
                "href": "/api/users/" // !!!!!!!!!!!!!!!!!!!!!!!!
              }
            }
          }
        ```
        - Target (Цель) — указана в качестве URI
        - Relation (Отношение) — имя
      - **Embedded Resources (Встроенные ресурсы):** другие ресурсы, содержащиеся в данном REST 
        ресурсе.
        ```js
          {
            "id": 42,
            "first_name": "Adrien",
            "last_name": "Brault",
            "_links": {
              "self": {
                "href": "/api/users/42"
              },
              "users_amount": {
                "href": "/api/users/amount" 
              },
              "user_last": {
                "href": "/api/users/last" 
              },
              "users": {
                "href": "/api/users/" 
              }
            },
            "embedded": { // !!!!!!!!!!!!!!!!!!!!!!!!
              "city": {
                "_links": {
                  "self": {
                    "href": "http://cities/user/42"
                  },
                  "cities": {
                    "href": "http://cities"
                  }
                  "capital": {
                     "href": "http://cities/capital"
                  }
                }, 
                "id": "d26d453fg32df5",
                "name": "Kharkiv"
              },
              "job": {
                "_links": {
                  "self": {
                    "href": "http://jobs/user/42"
                  },
                  "jobs": {
                    "href": "http://jobs"
                  }
                  "top_jobs": {
                    "href": "http://jobs/top"
                  }
                }, 
                "id": "26cfg46cv454",
                "company": "Google",
                "position": "Developer"
              },
            },
          }
        ```       
        - State (Состояние): фактические данные ресурса
     
   ![link](https://drive.google.com/uc?id=1Gsm0CLWR7G84Qi03RNgYx1_EoKsD_kEY)
     
### 5) Layered System (Не путать в Layered API architecture)
В REST допускается разделить систему на иерархию слоев но с условием, что каждый компонент
может видеть компоненты только непосредственно следующего слоя. REST allows you to use a layered
system architecture where you deploy the APIs on server A, and store data on server B and 
authenticate requests in Server C, for example. A client cannot ordinarily tell whether it is
connected directly to the end server or an intermediary along the way.
![link](https://miro.medium.com/max/1276/1*qpp130avfimrvKOHqCwGtg.jpeg)

###  6) Code-On-Demand (опционально)
В REST позволяется загрузка и выполнение кода или программы на стороне клиента.
Серверы могут временно расширять или кастомизировать функционал клиента, передавая ему 
логику, которую он может исполнять. Например, это могут быть скомпилированные Java-апплеты 
или клиентские скрипты на Javascript