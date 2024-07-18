Что должно сопровождать создание сервиса, чтобы не болела голова у сисадмина и девопса по поддержанию его работоспособности.

## Затравка (описание проблемы)

Устанавливаем сервис, настраиваем его (порты, доступ к сервису, пользователи, настройки памяти и хранилища), начинаем эксплуатировать. Но иногда то забудем настроить бакап, то забудем настроить HA-LB, то логи забудем настроить ротейтилку им и они засрут через полгода место, то настройку его сделаем "вручную" (без оркистратора), ну и мониторинг понятное дело - оставим напотом и забудем.
А потом, через N месяцев случается хня и нам (сисадминам) становится обидно, что или не сделали бакап вовремя, или бакап не проверили (а там хрень), или логи засрали всё место (так что сервис аж остановился), или логи засрали всё место по причине отсутствия мониторинга, или несмотря на то, что данные сохранились, но пропали учётные записи пользователей, работающих с данным сервисом...
Хотелось бы избавиться от этих неприятностей.

# Некоторые определения
(нет слова - нет знания)
### Сервис
Программный продукт, предоставляющий "наружу" (относительно себя) свои возможности через сетевой или локальный интерфейс (ipv4, unix).
Обладает настройками, кодом (своими библиотеками), может обладать хранилищем.
Способен взаимодействовать с другими сервисами (анонимная или персонифицированная внешняя интеграция).
### BLM (backup-logging-monitoring)
Основные элементы сопровождения сервиса со стороны сисадмина/девопса : резервное копирование (backup), обработка логов (logging), мониторинг и алёртинг (monitoring)

## Рассмотрим приложение frontend+backend+db
Что ещё, кроме его подъёма при помощи docker-compose, нужно сделать, чтобы не волноваться про него в будущем?
	- управление конфигурациями приклада и секретами, развёртывание, оркестрирование
	- BLM (backup+logging+monitoring) (для БД - backup+replica+test)
	- CICD (continuous integration+delivery)
	- тестирование (smoke, healthcheck, нагрузочное, регрессионное, юнит-тесты, интеграционное)
	- управление пользователями (zitadel?)
	- управление рутинными задачами (kestra.io?)
	- внешние интеграции (почта?)

# Управление конфигурациями приклада


Далее...

# Комментарии

### Комментарии от Павла
* нужно квотировать после нагрузочного обязательно. 
* Кроме того обозначить метрики и триггеры алертов именно выделить в обязательное условие приема на саппорт (в прод).  Иначе головняки будут обязательно. 
* Также про бэкапы - нужно генерить сразу требования к описанию оных. Как то: Что именно бэкапим, каким методом: icrement, diff, full. Обязательно план восстановления с тестированием и итогами тестового восстановления.
* Это (шпаргалки по InfraOps) описано, понятное дело, чаще всего в релгаментах внутренних и регуляторке типа ЦБ, и прочем. В остальном в сети разровненная инфа, котора подразумевает наличие у админа здравого смысла и опыта коть какого-то
* Практики как таковые - ХЗ. Всё зависит от того, что бэкапить. Вангую, если важная data, database, то diff предпочтительнее, но дороже в хранении. Тут всё зависит от возможности, ресурсов и здравого смысла, опять же)) . Ну и регуляторки давления тоже.

### Комментарии от Александра
* (про сгенерённое ИИ) Нарм, только Swarm нинужон
* И я бы добавил InfraOps и выкинул бы Jenkins
* В Performance Tuning маловато...
* И что-нибудь про постмортемы еще нужно прикрутить и про алерты

# Ссылочки из канала

https://gitinsky.com/infra-ops
тут про термин InfraOps

https://roadmap.sh/r/application-deployment-and-management
Это я попросил ИИ накидать roadmap.sh - как заготовка плана - вышло зачотно.
(но я чуть позже нечаянно испортил внешний вид)

# Авторы
Иван Грушин и AI (заготовка roadmap.sh).
Дополнения и комментарии:  Дмитрий Николаев, Alex, Павел Тихонюк, Александр Чистяков.

# ====================


Ai-generated plan of learning.
https://roadmap.sh/r/application-deployment-and-management

## Fundamentals of application deployment

#### Understanding software deployment
Приложения как бинарник и как контейнер
#### Application packaging standards
#### Deployment strategies
#### VCS: version control systems
#### Continuous Integration & continuous deployment (CI/CD)
#### Basics of Docker


## Infrastructure setup

#### Infrastructure basics
#### Infrastructure as a code (IaC, IaaC)
#### Understanding cloud platforms
#### Server configuration
#### Load balancing and auto-scaling
#### Containerization and virtualization


## Backup and recovery
#### Importance of backup and recovery
#### Data backup strategies
#### Backup software tools
#### Implementing automatic backups
#### Data recovery strategies
#### Validating and testing backups


## Implementing logging
#### Introduction to system logging
#### The log files and syslog standard
#### Log management tools
#### Centralized logging
#### Analyzing and managing logs
#### Log monitoring and alerting


## System and application monitoring
#### Monitoring basics
#### System monitoring tools
#### Application performance monitoring (APM)
#### Network monitoring
#### Cloud monitoring
#### Setting up monitoring dashboards

## User management
#### Understanding access control
#### Basics of user management
#### Implementing user authentication
#### Implementing user authorization
#### User role management
#### User priveledge auditing


## Security
#### Basics of information security
#### Working with firewalls
#### Implementing intrusion detection systems
#### Security connectivity with VPNs
#### Web security best practices
#### Cybersecurity awareness and practices


## Orchestration
#### Basics of orcestration
#### Cluster management and orchestration
#### Docker swarm
#### Kubernetes basics
#### Kubernetes deployment
#### Advanced kubernetes management


## Scripting and automation
#### Understanding scripting basics
#### Using bash for scripting
#### Python for automation
#### Using ansible for configuration management
#### Using Terraform for IaC
#### Using Jenkins for CI/CD automation


## Performance tuning
#### Basics of performance tuning
#### Optimizing database performance
#### Optimizing server performance
#### Application optimization
#### Network optimization
#### Implementing caching mechanisms



## Troubleshooting
#### Basics of troubleshooting
#### Network troubleshooting
#### System troubleshooting
#### Application troubleshooting
#### Troubleshooting common security issues
#### Documenting and reporting issues


## Maintenance and updates
#### Importance of regular maintenance
#### Planning and implementing updates
#### Managing downtimes
#### Patch management
#### Ensuring high availability (HA)
#### Lifecycle management
