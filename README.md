# 6.1. Типы и структура СУБД
## 1.
- Электронные чеки в json виде я думаю подойдет MongoDB как один их представителей NOSQL
- Склады и автомобильные дороги для логистической компании я думаю тут подойдет одна из Реляционные базы данных типо MSSQL, MYSQL, PostgreSQL
- Генеалогические деревья я думаю подойдет Графовая база данных 
- Кэш идентификаторов клиентов с ограниченным временем жизни для движка аутенфикации Redis Резидентная база данных
- Отношения клиент-покупка для интернет-магазина я думаю тут подойдет одна из Реляционные базы данных типо MSSQL, MYSQL, PostgreSQL

## 2.
- Данные записываются на все узлы с задержкой до часа (асинхронная запись) -я думаю подойдет Система класса CP в каждый момент обеспечивает целостный результат и способна функционировать в условиях распада, но достигает этого в ущерб доступности.   (PC/EC)
- При сетевых сбоях, система может разделиться на 2 раздельных кластера - В системе класса CA во всех узлах данные согласованы и обеспечена доступность, при этом она жертвует устойчивостью к распаду на секции. (PC/EL)
- Система может не прислать корректный ответ или сбросить соединение - В системе класса AP не гарантируется целостность, но при этом выполнены условия доступности и устойчивости к распаду на секции. (PA/EL)

## 3.
По сути, чем отличаются БД ACID от не-ACID, так это тем, что не-ACID фактически отказываются от обеспечения изоляции. Принципы BASE значительно слабее гарантий ACID, и между ними нет прямого соответствия. BASE-хранилища обеспечивают менее строгий контроль: данные будут согласованы позднее, вероятнее всего, во время чтения, или всегда будут согласованы, но только для определенных фиксаций, обработанных последними. Учитывая свой собстевнный опыт, скорее всего их нельзя вместе использовать. 
## 4.
Pub-Sub поведенчиский шаблон проектирования передачи сообщений, в котором отправители сообщений, именуемые издателями напрямую не привязаны программным кодом отправки сообщений к подписчикам.  Вместо этого сообщения делятся на классы и не содержат сведений о своих подписчиках. Все участники оперируют с сообщениями. Сообщения — это передаваемые данные. Обычно это просто массив байт, в который сериализуются любые данные.
Основной проблемой это Очередь — это временное хранилище сообщений, работающее на принципе «Первый пришёл — первый ушёл». 
Pub-sub система — это централизованный платный сервис, брокер, через который и проходят все сообщения.
Я думаю подходит REDIS
Redis вообще-то не pub-sub система, а key-value data storage. Но он на удивление хорошо реализует классический pub-sub и показывает замечательную производительность.
Вы можете установить Redis локально или как распределенный сервис. Вы можете добавить возможность сохранения сообщений на диск.