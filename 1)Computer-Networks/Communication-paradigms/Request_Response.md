# Request-Response

Основополагающим свойством системы обмена сообщениями является направленность 
связи, которая обычно определяется ее семантикой:

## 1) Однонаправленный:
**Однонаправленный** (электронная почта или веб-сервер, который отправляет 
сообщения подключенному браузеру с помощью веб-сокетов, или система, 
распределяющая задания между группой рабочих процессов):

![link](https://drive.google.com/uc?id=1H9TxiK11uZ6_cHaT8y_lbZ-MQo7Zfk9v)

## 2) Двунаправленный "Request-Response" (HTTP):

![link](https://drive.google.com/uc?id=1wNxXb6-dMN2gpH2kZ-xWwd-iowYUW5hv)  

![link](https://drive.google.com/uc?id=113Ql0G1U9Vd-6fndY_dpItwQOfhQlZd_)

### Synchronous / Asynchronous:
When a client and service interact using either request/response or asynchronous
request/response, the client sends a request and the service sends back a reply. 
The difference between the two interaction styles is that with request/response the client
expects the service to **respond immediately,** whereas with asynchronous request/
response there is **no such expectation.** Messaging is inherently asynchronous, so only
provides asynchronous request/response. But a client could block until a reply is
received.