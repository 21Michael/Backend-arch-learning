# Session Layer

**Сеансовый уровень (Session layer)** — 5-й уровень сетевой модели OSI, отвечает за
поддержание сеанса связи, позволяя приложениям взаимодействовать между собой
длительное время. Уровень управляет созданием/завершением сеанса, обменом
информацией, синхронизацией задач, определением права на передачу данных и
поддержанием сеанса в периоды неактивности приложений. Синхронизация передачи
обеспечивается помещением в поток данных контрольных точек, начиная с которых
возобновляется процесс при нарушении взаимодействия.

Сеансы передачи составляются из запросов и ответов, которые осуществляются между
приложениями. В случае потери соединения этот протокол может попытаться его
восстановить. Если соединение не используется длительное время, то протокол сеансового
уровня может его закрыть и открыть заново. Он позволяет производить передачу в
дуплексном или в полудуплексном режимах и обеспечивает наличие контрольных точек в
потоке обмена сообщениями.

## Виды протоколов сеансового уровня:

##PPTP (Point-to-Point Tunneling Protocol)

**PPTP (Point-to-Point Tunneling Protocol)** — туннельный протокол типа точка-точка,
позволяющий компьютеру устанавливать защищённое соединение с сервером за счёт
создания специального туннеля в стандартной, незащищённой сети. PPTP помещает
(инкапсулирует) кадры PPP в IP-пакеты для передачи по глобальной IP-сети, например
Интернет. PPTP может также использоваться для организации туннеля между двумя
локальными сетями. РРТР использует дополнительное TCP-соединение для обслуживания
туннеля.

## L2TP (Layer 2 Tunneling Protocol)

**L2TP (Layer 2 Tunneling Protocol — протокол туннелирования второго уровня)** — в
компьютерных сетях туннельный протокол, использующийся для поддержки виртуальных
частных сетей. Главное достоинство L2TP состоит в том, что этот протокол позволяет
создавать туннель не только в сетях IP, но и в таких, как ATM, X.25 и Frame Relay.