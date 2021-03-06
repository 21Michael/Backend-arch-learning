# HTTP

**Протокол передачи гипертекста (Hypertext Transfer Protocol - HTTP)** - это прикладной протокол
для передачи гипертекстовых документов, таких как HTML. Он создан для связи между веб-браузерами и
веб-серверами, хотя в принципе HTTP может использоваться и для других целей. Протокол следует
классической клиент-серверной модели, когда клиент открывает соединение для создания запроса, а
затем ждёт ответа. HTTP - это протокол без сохранения состояния, то есть сервер не сохраняет
никаких данных (состояние) между двумя парами "запрос-ответ". Несмотря на то, что HTTP основан
на TCP/IP, он также может использовать любой другой протокол (UDP) транспортного уровня с гарантированной
доставкой.

Между веб-браузером и сервером находятся большое количество сетевых узлов, передающих HTTP
сообщения. Из-за слоистой структуры большинство из них оперируют также на транспортном сетевом
или физическом уровнях, становясь прозрачным на HTTP слое и потенциально снижая производительность.
Эти операции на уровне приложений называются прокси.

![link](https://mdn.mozillademos.org/files/13679/Client-server-chain.png)

###Характеристики:
- **Простота**  
  HTTP-сообщения могут читаться и пониматься людьми, обеспечивая более лёгкое тестирование
  разработчиков и уменьшенную сложность для новых пользователей.

- **Расширяемость**  
  Введённые в HTTP/1.0 HTTP-заголовки сделали этот протокол лёгким для расширения и
  экспериментирования. Новая функциональность может быть даже введена простым соглашением
  между клиентом и сервером о семантике нового заголовка.

- **Не имеет состояния, но имеет сессию**   
  HTTP не имеет состояния: **не существует связи между двумя запросами, которые последовательно
  выполняются по одному соединению.** Из этого немедленно следует возможность проблем для
  пользователя, пытающегося взаимодействовать с определённой страницей последовательно, например,
  при использовании корзины в электронном магазине. Но хотя ядро HTTP не имеет состояния,
  куки позволяют использовать сессии с сохранением состояния. Используя расширяемость заголовков,
  **куки добавляются к рабочему потоку, позволяя сессии на каждом HTTP-запросе делиться некоторым
  контекстом или состоянием.**
- **TCP соединение**  
  Соединение управляется на транспортном уровне, и потому принципиально выходит за границы HTTP.
  Хотя HTTP не требует, чтобы базовый транспортного протокол был основан на соединениях, требуя
  только надёжность, или отсутствие потерянных сообщений (т.е. как минимум представление ошибки).
  Среди двух наиболее распространённых транспортных протоколов Интернета, TCP надёжен, а UDP —
  нет. HTTP впоследствии полагается на стандарт TCP, являющийся основанным на соединениях,
  несмотря на то, что соединение не всегда требуется.

## 1. HTTP messages:

**1. REQUEST:**

![link](https://mdn.mozillademos.org/files/13687/HTTP_Request.png)

**Запросы содержат следующие элементы:**
- **HTTP-метод,** определяющее операцию, которую клиент хочет выполнить. Обычно, клиент хочет
  получить ресурс (используя GET) или передать значения HTML-формы (используя POST), хотя другие
  операция могут быть необходимы в других случаях.
- **Путь к ресурсу: URL** ресурсы лишены элементов, которые очевидны из контекста, например без
  protocol (http://), domain (здесь developer.mozilla.org), или TCP port (здесь 80).
- **Версию HTTP-протокола.**
- **Заголовки (опционально),** предоставляющие дополнительную информацию для сервера.
- **Тело,** для некоторых методов, таких как POST, которое содержит отправленный ресурс.


**2. RESPONSE:**

![link](https://mdn.mozillademos.org/files/13691/HTTP_Response.png)

**Ответы содержат следующие элементы:**
- **Версию HTTP-протокола.**
- **HTTP код состояния,** сообщающий об успешности запроса или причине неудачи.
- **Сообщение состояния** — краткое описание кода состояния.
- **HTTP заголовки,** подобно заголовкам в запросах.
- **Тело,** содержащее пересылаемый ресурс.

## 2. Cache:

Производительность веб-сайтов и приложений можно значительно повысить за счёт повторного 
использования ранее полученных ресурсов. Веб-кеши сокращают задержку и снижают сетевой трафик,
уменьшая тем самым время, необходимое для отображения ресурсов. Используя HTTP-кеширование, 
сайты становятся более отзывчивыми.

### Виды кеширования:
  - **Приватные кеши:**  
    Приватный кеш предназначен для отдельного пользователя. Вы, возможно, уже видели параметры 
    кеширования в настройках своего браузера. Кеш браузера содержит все документы, загруженные 
    пользователем по HTTP. Он используется для доступа к ранее загруженным страницам при навигации
    назад/вперёд, позволяет сохранять страницы, или просматривать их код, не обращаясь лишний раз
    к серверу. Кроме того, кеш полезен при отключении от сети.
  - **Кеши совместного использования:**  
    Кеш совместного использования — это кеш, который сохраняет ответы, чтобы их потом могли 
    использовать разные пользователи. Например, в локальной сети вашего провайдера или компании,
    может быть установлен прокси, обслуживающий множество пользователей, чтобы можно было повторно 
    использовать популярные ресурсы, сокращая тем самым сетевой трафик и время ожидания.

![link](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching/http_cache_type.png)

### Цели кеширования:
**Примеры того, что обычно записывается в кеш:**

  - Успешно загруженные ресурсы: ответ 200 OK на запрос методом GET HTML-документов, изображений
    или файлов.
  - Постоянные перенаправления: ответ 301 Moved Permanently («перемещено навсегда»).
  - Сообщения об ошибках: ответ 404 Not Found («не найдено»).
  - Неполные результаты: ответ 206 Partial Content («частичное содержимое»).
  - Ответы на запросы отличные от GET, если есть что-либо, подходящее для использования в 
    качестве ключа кеша.
    
### Что можно кешировать:
  - Метод, используемый в запросе, кешируемый, если это GET или HEAD. Ответ для POST или PATCH
    запросов может также быть закеширован, если указан признак "свежести" данных и установлен 
    заголовок Content-Location (en-US), но это редко реализуется. (Например, Firefox не 
    поддерживает это согласно https://bugzilla.mozilla.org/show_bug.cgi?id=109553.) Другие методы,
    такие как PUT и DELETE не кешируемые, и результат их выполнения не кешируется.
  - Коды ответа, известные системе кеширования, которые рассматриваются как кешируемые: 200, 
    203, 204, 206, 300, 301, 404, 405, 410, 414, 501.

### Управление кешированием (заголовок Cache-control):
  - **отсутствие кеширования:**  
    В кеше не должно сохраняться ничего — ни по запросам клиента, ни по ответам сервера.
    Запрос всегда отправляется на сервер, ответ всегда загружается полностью.
    
    ```http request
      Cache-Control: no-store
      Cache-Control: no-cache, no-store, must-revalidate
    ```
    
  - **Кешировать, но проверять актуальность:**  
    Перед тем, как выдать копию, кеш запрашивает исходный сервер на предмет актуальности ресурса.
    
     ```http request
       Cache-Control: no-cache
     ```
    
  - **Приватные (private) и общие (public) кеши:**  
    Директива "public" указывает, что ответ можно сохранять в любом кеше. Это бывает полезно,
    если возникает потребность сохранить страницы с HTTP-аутентификацией, или такими кодами 
    ответа, которые обычно не кешируются. Директива же "private" указывает, что ответ предназначен
    отдельному пользователю и не должен храниться в кеше совместного использования. В этом случае 
    ответ может сохраняться приватным кешем браузера.
    
     ```http request
       Cache-Control: private
       Cache-Control: public
     ```
    
  - **Срок действия (Expiration):**  
    Самой важной здесь является директива "max-age=<seconds>" — максимальное время, в течение
    которого ресурс считается "свежим". В отличие от директивы Expires, она привязана к моменту
    запроса.
    
     ```http request
      Cache-Control: max-age=31536000
     ```
    
  - **Проверка актуальности:**  
    При использовании директивы "must-revalidate" кеш обязан проверять статус ресурсов с 
    истёкшим сроком действия. Те копии, что утратили актуальность, использоваться не должны.
    
    ```http request
      Cache-Control: must-revalidate
    ```

## 3. METHODS:

###Характеристики HTTP методов:  

  - **Безопасность:**  
    Метод HTTP является безопасным, если он не меняет состояние сервера. Другими словами, 
    безопасный метод проводит операции "только чтение" (read-only).  
    **Безопасные:** GET, HEAD, OPTIONS.
    **Не безопасные:** POST, CONNECT, PATCH, PUT, DELETE;
    
  - **Идемпотентность:**  
    Метод HTTP является идемпотентным, если повторный идентичный запрос, сделанный один или 
    несколько раз подряд, имеет один и тот же эффект, не изменяющий состояние сервера. Другими 
    словами, идемпотентный метод не должен иметь никаких побочных эффектов (side-effects), кроме 
    сбора статистики или подобных операций.  
    **Идемпотентные методы:** GET, HEAD, PUT и DELETE;  
    **Неидемпотентные методы:** POST, CONNECT, PATCH (инструкции в методе могут добавлять новые данные на
    сервер);  
    Также все безопасные методы являются идемпотентными.
  
  - **Кешируемость:**  
    Кешируемые ответы - это HTTP-ответы, которые могут быть закешированы, то есть сохранены для 
    дальнейшего восстановления и использования позже, тем самым снижая число запросов к серверу.
    Не все HTTP-ответы могут быть закешированы

### Методы:

![link](https://res.cloudinary.com/nlogn/images/w_547,h_356/f_auto,q_auto/v1587453297/HTTP-methods-comaprison/HTTP-methods-comaprison.png?_i=AA)

### - GET (получает данные)
**Метод GET запрашивает представление ресурса. Запросы с использованием этого метода могут только
извлекать данные.**

### - HEAD (получает хедер HTTP запроса)
**HEAD запрашивает ресурс так же, как и метод GET, но без тела ответа.**  

HTTP-метод HEAD запрашивает заголовки, идентичные тем, что возвращаются, если указанный ресурс
будет запрошен с помощью HTTP-метода GET. Такой запрос может быть выполнен перед загрузкой большого
ресурса, например, для экономии пропускной способности.

Ответ на метод HEAD не должен содержать тело. Если это не так, то его следует игнорировать. Но
даже в этом случае заголовки сущности, описывающие содержимое тела, например Content-Length, 
должны быть включены в ответ. Они не относятся к телу ответа на запрос HEAD, которое должно быть
пустым, они относятся к телу ответа, полученный на аналогичный запрос с помощью метода GET.

### - POST (создает новые данные)
**POST используется для отправки сущностей к определённому ресурсу. Часто вызывает изменение 
состояния или какие-то побочные эффекты на сервере.**

Тип тела запроса указывается в заголовке Content-Type.

### - PUT (если данные существуют полностью заменить на новые данные, если нет создать новые)
**PUT заменяет все текущие представления ресурса данными запроса.**

Метод запроса HTTP PUT создаёт новый ресурс или заменяет представление целевого ресурса, данными
представленными в теле запроса.

Разница между PUT и POST в том, что PUT является идемпотентным, т.е. единичный и множественные
вызовы этого метода, с идентичным набором данных, будут иметь тот же результат выполнения (без 
сторонних эффектов), в случае с POST, множественный вызов с идентичным набором данных может повлечь
за собой сторонние эффекты.

### - DELETE (удалить данные)
**DELETE удаляет указанный ресурс.**

### - CONNECT (двустороннее соединение)
**CONNECT устанавливает "туннель" к серверу, определённому по ресурсу.**

HTTP CONNECT method запускает двустороннюю связь с запрошенным ресурсом. Метод можно использовать 
для открытия туннеля.

К примеру, метод CONNECT может использоваться для доступа к сайту, который использует SSL (en-US)
(HTTPS). Клиент запрашивает HTTP-прокси-сервер для туннелирования TCP-соединения с желаемым 
назначением. За тем сервер переходит к подключению от имени клиента. После того, как соединение 
установлено сервером, прокси-сервер продолжает проксировать поток TCP к клиенту и от него.

### - OPTIONS (описание параметров соединения)
**OPTIONS используется для описания параметров соединения с ресурсом.**

HTTP-метод OPTIONS используется для описания параметров соединения с целевым ресурсом. 
Клиент может указать особый URL для обработки метода OPTIONS, или * (звёздочку) чтобы указать 
весь сервер целиком.

### - TRACE (проверка связи с сервером)
**TRACE выполняет вызов возвращаемого тестового сообщения с ресурса.**

HTTP Метод TRACE выполняет проверку обратной связи по пути к целевому ресурсу, предоставляя 
полезный механизм отладки.

Конечный получатель запроса должен отразить полученное сообщение, исключая некоторые поля
описанные ниже, назад клиенту как тело сообщения с ответом 200 (OK) с заголовком Content-Type 
message/http. Конечный получатель это либо исходный сервер, либо первый сервер получивший значение
Max-Forwards в запросе.

### - PATCH (частичное изменение данных)
**PATCH используется для частичного изменения ресурса.**

В какой-то степени PATCH можно назвать аналогом концепта «обновить» (update) из CRUD (en-US) 
(но не стоит путать HTTP и CRUD (en-US) — это две разные вещи).

PATCH может как быть идемпотентным, так и не быть, в отличие от PUT, который всегда идемпотентен.
Операция считается идемпотентной, если её многократное выполнение приводит к тому же результату,
что и однократное выполнение. Например, если автоинкрементное поле является важной частью ресурса,
то PUT перезапишет его (т.к. он перезаписывает всё), но PATCH может и не перезаписать.

PATCH (как и PUT) может иметь побочные эффекты на другие ресурсы.

Чтобы обозначить, что сервер поддерживает PATCH, можно добавить этот метод в список заголовков 
ответа Allow (en-US) или Access-Control-Allow-Methods (для CORS).

Другой (неявный) индикатор, что PATCH разрешён, является наличие заголовка Accept-Patch, где 
описано, в каком формате сервер принимает изменённые документы.

## 4. RESPONSE CODES:

Код ответа (состояния) HTTP показывает, был ли успешно выполнен определённый HTTP запрос.   

**Коды сгруппированы в 5 классов:**
  - Информационные 100 - 199
  - Успешные 200 - 299
  - Перенаправления 300 - 399
  - Клиентские ошибки 400 - 499
  - Серверные ошибки 500 - 599

### Информационные 100 - 199:
|Код ответа| Название|	Описание|	Версия HTTP|
|----------|---------|----------|------------|
|100|	Continue|	"Продолжить". Этот промежуточный ответ указывает, что запрос успешно принят и клиент может продолжать присылать запросы либо проигнорировать этот ответ, если запрос был завершён.|	Только HTTP/1.1|
|101|	Switching Protocol|	"Переключение протокола". Этот код присылается в ответ на запрос клиента, содержащий заголовок Upgrade:, и указывает, что сервер переключился на протокол, который был указан в заголовке. Эта возможность позволяет перейти на несовместимую версию протокола и обычно не используется.	|Только HTTP/1.1|
|102|	Processing|	"В обработке". Этот код указывает, что сервер получил запрос и обрабатывает его, но обработка ещё не завершена.	|Только HTTP/1.1|
|103|	Early Hints|	"Ранние подсказки". В ответе сообщаются ресурсы, которые могут быть загружены заранее, пока сервер будет подготавливать основной ответ. RFC 8297 (Experimental).	|Только HTTP/1.1|

### Успешные 200 - 299:
|Код ответа| Название|	Описание|	Версия HTTP|
|----------|---------|----------|------------|
|200| OK| "Успешно". Запрос успешно обработан. Что значит "успешно", зависит от метода HTTP, который был запрошен: - GET: "ПОЛУЧИТЬ". Запрошенный ресурс был найден и передан в теле ответа.- HEAD: "ЗАГОЛОВОК". Заголовки переданы в ответе. - POST: "ПОСЫЛКА". Ресурс, описывающий результат действия сервера на запрос, передан в теле ответа. - TRACE: "ОТСЛЕЖИВАТЬ". Тело ответа содержит тело запроса полученного сервером. |HTTP/0.9 и выше|
|201|	Created|	"Создано". Запрос успешно выполнен и в результате был создан ресурс. Этот код обычно присылается в ответ на запрос PUT "ПОМЕСТИТЬ".	|HTTP/0.9 и выше|
|202|	Accepted|	"Принято". Запрос принят, но ещё не обработан. Не поддерживаемо, т.е., нет способа с помощью HTTP отправить асинхронный ответ позже, который будет показывать итог обработки запроса. Это предназначено для случаев, когда запрос обрабатывается другим процессом или сервером, либо для пакетной обработки.	|HTTP/0.9 и выше|
|203|	Non-Authoritative Information|	"Информация не авторитетна". Этот код ответа означает, что информация, которая возвращена, была предоставлена не от исходного сервера, а из какого-нибудь другого источника. Во всех остальных ситуациях более предпочтителен код ответа 200 OK.	|HTTP/0.9 и 1.1|
|204|	No Content|	"Нет содержимого". Нет содержимого для ответа на запрос, но заголовки ответа, которые могут быть полезны, присылаются. Клиент может использовать их для обновления кешированных заголовков полученных ранее для этого ресурса.	|HTTP/0.9 и выше|
|205|	Reset Content|	"Сбросить содержимое". Этот код присылается, когда запрос обработан, чтобы сообщить клиенту, что необходимо сбросить отображение документа, который прислал этот запрос.	|Только HTTP/1.1|
|206|	Partial Content|	"Частичное содержимое". Этот код ответа используется, когда клиент присылает заголовок диапазона, чтобы выполнить загрузку отдельно, в несколько потоков.|	Только HTTP/1.1|

### Перенаправления 300 - 399:
|Код ответа| Название|	Описание|	Версия HTTP|
|----------|---------|----------|------------|
|300|	Multiple Choice| "Множественный выбор". Этот код ответа присылается, когда запрос имеет более чем один из возможных ответов. И User-agent или пользователь должен выбрать один из ответов. Не существует стандартизированного способа выбора одного из полученных ответов. |HTTP/1.0 и выше|
|301|	Moved Permanently| "Перемещён на постоянной основе". Этот код ответа значит, что URI запрашиваемого ресурса был изменён. Возможно, новый URI будет предоставлен в ответе. |HTTP/0.9 и выше|
|302|	Found| "Найдено". Этот код ответа значит, что запрошенный ресурс временно изменён. Новые изменения в URI могут быть доступны в будущем. Таким образом, этот URI, должен быть использован клиентом в будущих запросах. |HTTP/0.9 и выше|
|303|	See Other|	"Просмотр других ресурсов". Этот код ответа присылается, чтобы направлять клиента для получения запрашиваемого ресурса в другой URI с запросом GET.	|HTTP/0.9 и 1.1|
|304|	Not Modified|	"Не модифицировано". Используется для кеширования. Это код ответа значит, что запрошенный ресурс не был изменён. Таким образом, клиент может продолжать использовать кешированную версию ответа.	|HTTP/0.9 и выше|
|305|	Use Proxy|	"Использовать прокси". Это означает, что запрошенный ресурс должен быть доступен через прокси. Этот код ответа в основном не поддерживается из соображений безопасности.	|Только HTTP/1.1|
|306|	Switch Proxy|	Больше не использовать. Изначально подразумевалось, что " последующие запросы должны использовать указанный прокси."	|Только HTTP/1.1|
|307|	Temporary Redirect|	"Временное перенаправление". Сервер отправил этот ответ, чтобы клиент получил запрошенный ресурс на другой URL-адрес с тем же методом, который использовал предыдущий запрос. Данный код имеет ту же семантику, что код ответа 302 Found, за исключением того, что агент пользователя не должен изменять используемый метод HTTP: если в первом запросе использовался POST, то во втором запросе также должен использоваться POST.	|Только HTTP/1.1|

### Клиентские ошибки 400 - 499:
|Код ответа| Название|	Описание|	Версия HTTP|
|----------|---------|----------|------------|
|400|	Bad Request|	"Плохой запрос". Этот ответ означает, что сервер не понимает запрос из-за неверного синтаксиса. 	|HTTP/0.9 и выше|
|401|	Unauthorized|	"Неавторизованно". Для получения запрашиваемого ответа нужна аутентификация. Статус похож на статус 403, но,в этом случае, аутентификация возможна. 	|HTTP/0.9 и выше|
|402|	Payment Required|	"Необходима оплата". Этот код ответа зарезервирован для будущего использования. Первоначальная цель для создания этого когда была в использовании его для цифровых платёжных систем(на данный момент не используется).	|HTTP/0.9 и 1.1|
|403|	Forbidden|	"Запрещено". У клиента нет прав доступа к содержимому, поэтому сервер отказывается дать надлежащий ответ. 	|HTTP/0.9 и выше|
|404|	Not Found|	"Не найден". Сервер не может найти запрашиваемый ресурс. Код этого ответа, наверно, самый известный из-за частоты его появления в вебе. 	|HTTP/0.9 и выше|
|405|	Method Not Allowed|	"Метод не разрешён". Сервер знает о запрашиваемом методе, но он был деактивирован и не может быть использован. Два обязательных метода,  GET и HEAD,  никогда не должны быть деактивированы и не должны возвращать этот код ошибки.	|Только HTTP/1.1|
|406|	Not Acceptable| Этот ответ отсылается, когда веб сервер после выполнения server-driven content negotiation, не нашёл контента, отвечающего критериям, полученным из user agent. |Только HTTP/1.1|
|407|	Proxy Authentication Required|	Этот код ответа аналогичен коду 401, только аутентификация требуется для прокси сервера.	|Только HTTP/1.1|
|408|	Request Timeout|	Ответ с таким кодом может прийти, даже без предшествующего запроса. Он означает, что сервер хотел бы отключить это неиспользуемое соединение. Этот метод используется все чаще с тех пор, как некоторые браузеры, вроде Chrome и IE9, стали использовать HTTP механизмы предварительного соединения для ускорения сёрфинга  (смотрите баг 634278, будущей реализации этого механизма в Firefox). Также учитывайте, что некоторые серверы прерывают соединения не отправляя подобных сообщений.	|Только HTTP/1.1|
|409|	Conflict| Этот ответ отсылается, когда запрос конфликтует с текущим состоянием сервера. |Только HTTP/1.1|
|410|	Gone| Этот ответ отсылается, когда запрашиваемый контент удалён с сервера. |Только HTTP/1.1|
|411|	Length Required| Запрос отклонён, потому что сервер требует указание заголовка Content-Length, но он не указан. |Только HTTP/1.1|
|412|	Precondition Failed|	Клиент указал в своих заголовках условия, которые сервер не может выполнить	|Только HTTP/1.1|
|413|	Request Entity Too Large| Размер запроса превышает лимит, объявленный сервером. Сервер может закрыть соединение, вернув заголовок Retry-After |Только HTTP/1.1|
|414|	Request-URI Too Long|	URI запрашиваемый клиентом слишком длинный для того, чтобы сервер смог его обработать	|Только HTTP/1.1|
|415|	Unsupported Media Type|	Медиа формат запрашиваемых данных не поддерживается сервером, поэтому запрос отклонён	|Только HTTP/1.1|
|416|	Requested Range Not Satisfiable|	Диапазон указанный заголовком запроса Range не может быть выполнен; возможно, он выходит за пределы переданного URI	|Только HTTP/1.1|
|417|	Expectation Failed|	Этот код ответа означает, что ожидание, полученное из заголовка запроса Expect, не может быть выполнено сервером.|	Только HTTP/1.1|

### Серверные ошибки 500 - 599:
|Код ответа| Название|	Описание|	Версия HTTP|
|----------|---------|----------|------------|
|500|	Internal Server Error|	"Внутренняя ошибка сервера". Сервер столкнулся с ситуацией, которую он не знает как обработать. 	|HTTP/0.9 и выше|
|501|	Not Implemented|	"Не выполнено". Метод запроса не поддерживается сервером и не может быть обработан. Единственные методы, которые сервера должны поддерживать (и, соответственно, не должны возвращать этот код) -  GET и HEAD.	|HTTP/0.9 и выше|
|502|	Bad Gateway|	"Плохой шлюз". Эта ошибка означает что сервер, во время работы в качестве шлюза для получения ответа, нужного для обработки запроса, получил недействительный (недопустимый) ответ. 	|HTTP/0.9 и выше|
|503|	Service Unavailable|	"Сервис недоступен". Сервер не готов обрабатывать запрос. Зачастую причинами являются отключение сервера или то, что он перегружен. Обратите внимание, что вместе с этим ответом удобная для пользователей(user-friendly) страница должна отправлять объяснение проблемы.  Этот ответ должен использоваться для временных условий и Retry-After: HTTP-заголовок должен, если возможно, содержать  предполагаемое время до восстановления сервиса. Веб-мастер также должен позаботиться о заголовках, связанных с кешем, которые отправляются вместе с этим ответом, так как эти ответы, связанные с временными условиями, обычно не должны кешироваться. |	HTTP/0.9 и выше|
|504|	Gateway Timeout|	Этот ответ об ошибке предоставляется, когда сервер действует как шлюз и не может получить ответ вовремя.	|Только HTTP/1.1|
|505|	HTTP Version Not Supported|	"HTTP-версия не поддерживается". HTTP-версия, используемая в запросе, не поддерживается сервером.	|Только HTTP/1.1|

## 5. HTTP 1.1 vs HTTP 2.0:

Новый протокол разработан для существенного улучшения работы веб-сайтов. Переход на http/2
имеет смысл, потому что он обладает рядом преимуществ:
- **Добавлены новые методы согласования протокола.** Как клиент, так и сервер имеют возможность
  пользоваться первой, второй версией HTTP и совершенно другими протоколами.
- **Поддержка совместимости с большим количеством функций HTTP 1.1.** К примеру, совместимость по
  виду URI, изобилию заголовков, набору методов доступа (POST, GET и т.д.), статусным кодам.
- **Ускорение загрузки документов.** Обеспечивается за счет сжатия HTTP-заголовков, конвейеризации
  запросов, применении push-технологий на сервере, устранении блокировки начала строки в
  протоколах 1.0 и 1.1, а также мультиплексировании нескольких запросов лишь в одном соединении.
- **Сохранение совместимости с площадками, где внедрен HTTP.** Это полные и мобильные версии
  браузеров, многие интерфейсы и сервера, в числе которых прокси-сервера.

**Нововведения:**
1. **Мультиплексирование**  
   В предыдущей версии для одного запроса была необходима установка отдельного TCP-соединения.
   И чем больше было запросов, тем медленней работал браузер. Благодаря мультиплексированию
   браузер отправляет сразу несколько запросов через одно TCP-соединение.

   Современные браузеры задействуют ограниченное число TCP-соединений, что не позволяет им
   быстро загружать «тяжелые» страницы. А http/2, где внедрена технология мультиплексирования,
   дает возможность загружать большое количество статического контента одновременно, существенно
   повышая производительность.

   ![link](https://freecontent.manning.com/wp-content/uploads/mentalmodel-HTTP2_in_Action2.png)

2. **Приоритезация**  
   Суть заключается в том, что браузер запрашивает у сервера отдельную загрузку некоторых
   элементов контента, к примеру, сначала скриптов JavaScript, а затем изображений.

   Приоритезация в протоколе не обязательна, но рекомендована, потому что мультиплексирование
   не способно полноценно работать без приоритетов.

3. **Сжатие заголовков HTTP (header compression)**
4. **Двоичный уровень кадрирования (binary lvl of coding)**  
   В отличие от HTTP/1.1, в котором все запросы и ответы хранятся в простом текстовом формате,
   HTTP/2 использует двоичный уровень кадрирования для инкапсуляции всех сообщений в двоичном
   формате, при этом сохраняя семантику HTTP (методы, заголовки). API прикладного уровня
   по-прежнему создает сообщения в обычных форматах HTTP, но нижележащий уровень преобразовывает
   эти сообщения в двоичные. Благодаря этому веб-приложения, созданные до HTTP/2, могут
   продолжать работать как обычно при взаимодействии с новым протоколом.