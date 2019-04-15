# Техническое задание

## Глоссарий

Профиль пользователя - информация о пользователе.

Аватар пользователя - фотография пользователя или любое другое изображение, которое пользователь использует в качестве изображения,
ассоциированного с его профилем.

Учебная задача - задача, которую пользователю необходимо выполнить в рамках прохождения некоторого учебного курса.

Карточка задачи - полное описание задачи и ее параметров.

Доска - абстракция физической доски, содержащей карточки задач.

Программный интерфейс приложения (Application Programming Interface, API) - набор вызовов для взаимодействия с сервером.

Сервер - программное обеспечение, выполняющее обработку и хранение данных пользователей.

Клиент - программное обеспечение, выполняющее отображение пользовательского интерфейса системы
и запросы к серверу на обработку данных.

Веб-приложение, система, сервис - в данном документе указанные термины взаимозаменяемы,
за исключением случаев когда обратное указано явно.

Одностраничное приложение (Single Page Application, SPA) - клиент, при функционировании которого страницы формируются в браузере без обращения к серверу.

## 1. Введение

### 1.1. Наименование разработки
Предметом разработки является веб-приложение StudTool - сервис для студентов,
позволяющий сохранять учебные материалы и обмениваться ими с другими пользователями,
а также предоставляющий инструменты для управления учебными задачами и контроля их выполнения.

### 1.2. Назначение разработки

#### 1.2.1. Краткое описание предметной области
В настоящий момент ведение конспектов лекций студентами осуществляется как с использованием бумажных носителей,
так и с использование персональных компьютеров, позволяющих ускорить процесс фиксирования информации и производить быстрый
обмен информацией с коллегами.

Основными недостатками ведения конспекта лекций на бумажном носителе являются:
1. невозможность восстановления в случае потери, повреждения носителя;
2. низкая скорость записи слов, необходимость использования сокращений, понижающая скорость чтения.

Существующие системы создания и редактирования документов, рассмотренные далее, могут оказаться неудобными
для решения поставленной задачи, по ряду причин:
1. как правило, универсальные системы сложны в освоении и требуют дополнительных усилий для изучения;
2. не предоставляют возможностей коллективного редактирования документа;
3. требуют интеграции со сторонними инструментами для добавления нужного функционала.

#### 1.2.2. Существующие аналоги
Среди основных аналогов можно выделить:
1. Evernote:
- базовый функционал предоставляется бесплатно;
- поддерживается вставка изображений и аудиозаписей в документ;
- имеется встроенный чат;
- имеется возможность совместного (не одновременного) редактирования документа;
2. MWeb:
- использование приложения является платным;
- в качестве языка разметки испозьзуется Markdown;
- позволяет экспортировать документ в различные форматы, включая PDF;
3. Google Docs:
- базовый функционал предоставляется бесплатно;
- имеется возможность совместного одновременного редактирования документа;
- имеется интеграция с Google Drive для хранение документов;
4. Trello:
- имеются доски для разделения задач по категориям;
- базовый функционал предоставляется бесплатно;

Данный проект должен иметь следующий функционал, позволяющий выделить его среди аналогов:
1. использование Markdown в качестве языка разметки;
2. возможность добавления изображения в документ;
3. использование досок для визуализации задач;
4. возможность авторизации через социальную сеть ВКонтакте (ВК);
5. использование открытых публичный программных интерфейсов (API) ВК для расширения функционала системы.

## 2. Описание системы

Проект представляет собой клиент-серверное приложение. Сервер предоставляет набор открытых методов (API), позволяющих
использовать различные клиенты (веб-браузер, мобильное приложение) для взаимодействия конечного пользователя с системой.
Разработка и эксплуатация системы происходят в соответствии с практиками DevOps и использованием гибких методологий разработки.

## 3. Требования к системе

### 3.1. Требования к функциональным характеристикам
1. Разрабатываемое программное обеспечение должно обеспечивать функционирование системы в режиме 24/7/365 со среднегодовым временем
доступности не менее 99.5%.
2. Время восстановления системы после критического сбоя не должно превышать 45 минут.
3. Система должна поддерживать возможность вертикального и горизонтального масштабирования.
4. Система должна быть доступна для использования без деградации функционала не менее 80% целевой аудитории.
5. Система должна соответствовать принципам "приложения двенадцати факторов" (The Twelve-Factor App).

### 3.2. Функциональные требования к системе с точки зрения пользователя
Система должна обеспечивать следующие функции:
1. регистрация и авторизация пользователей;
2. разделение пользователей на две роли:
- авторизованные пользователи
- неавторизованные пользователи;
2. для авторизованных пользователей:
- редактирование профиля;
- просмотр открытых данных профилей других пользователей;
- добавление пользователей в список друзей;
- редактирование и сохранение документов на стороне сервера;
- просмотр документов, к которым пользователь имеет доступ;
- ограничение возможности просмотра документов пользователя;
- создание и редактирование досок с карточками задач, связанными с конкретным предметом;
3. для неавторизованных пользователей:
- просмотр открытых данных профилей других пользователей;
- просмотр открытых документов других пользователей.

## 4. Входные параметры системы

1. Данные регистрации пользователей в формате JSON:
- адрес электронной почты пользователя (email, RFC 5322);
- пароль пользователя (не менее 8 символов и не более 64 символов)

2. Данные профилей пользователя в формате JSON:
- уникальное имя пользователя в системе (содержит буквы латинского алфавита,
цифры, символы "точка", не менее 1 символа и не более 32 символов);
- полное имя пользователя (не менее 1 символа и не более 128 символов);
- дата рождения пользователя (в формате гггг-мм-дд, например 1970-01-01);
- информация об учебном заведении:
  + наименование (не менее 1 не более 128 символов);
  + факультет (не менее 1 не более 128 символов);
  + кафедра (не менее 1 не более 128 символов);
  + год поступления;
  + год окончания.

3. Аватар пользователя - изображение в формате JPEG, размером не более 1Мб.

4. Документ пользователя - файл, содержащий разметку Markdown, размером не более 4Мб.

5. Карточка задачи по предмету в формате JSON:
- предмет (не менее 1 не более 64 символов);
- заголовок (не менее 1 не более 128 символов);
- описание (текст не менее 1 не более 4096 символов);
- дата сдачи задачи (в формате гггг-мм-дд, например 2020-01-01).

## 5. Выходные параметры системы

Выходными параметрами системы являются веб-страницы, содержащие следующую информацию:
- информация о профиле пользователя;
- список пользователей, с которыми пользователь состоит в отношении дружбы;
- доска с карточками задач по каждому предмету;
- карточка выбранной пользователем задачи;
- список документов, к которым пользователь имеет доступ;
- содержимое выбранного пользователем документа.

## 6. Требования к обеспечению безопасности
1. Система должна обрабатывать и хранить данные в соответствии с требованиями Общего регламента по защите данных (GDPR).
2. В системе должна быть предусмотрена защита от основных видов сетевых атак (DDOS, XSS, CSRF, SQL/NoSQL-инъекции).

## 7. Требования к составу и параметрам технических средств

Развертывание системы производится с использованием облачных платформ, в кластере из виртуальных машин, ресурсы каждой из которых
ограничены каждая объемом оперативной памяти - 1Гб; процессорные ядра - 1.

## 8. Требования к документации
Исполнитель должен подготовить следующие документы:
1. руководство по развертыванию системы;
2. документация к API в формате OpenAPI.

# Топология системы

![Alt text](https://github.com/studtool/assignment/blob/master/A.png)

## 1. Фронтенд-сервер
Служит единой точкой входа в систему. Реализует функции:
- аутентификация запроса;
- проксирование запроса на соответстующий сервис;
- отдача статического контента;
- фильтрация некорректных запросов.

## 2. Сервис авторизации
Хранит данные регистрации пользователя:
- адрес электоронной почты пользователя;
- пароль пользователя.

Реализует функции:
- регистрация пользователей;
- авторизация пользователей.

## 3. Сервис профилей
Хранит данные профилей пользователей:
- уникальное имя пользователя в системе;
- полное имя пользователя;
- дата рождения пользователя;
- информация об учебном заведении:
  + наименование;
  + факультет;
  + кафедра;
  + год поступления;
  + год окончания.

Выполняем функции:
- получение, изменение информации и пользователе;
- поиск пользователя с условиями фильтрации.

## 4. Сервис документов
Хранит аватары и документы пользователей.

Выполняет функции:
- хранение, изменение и отдача аватаров пользователей;
- хранение, изменение и отдача документов пользователей;
- получение списка документов пользователя;
- проверка прав пользователя на чтение и редактирование документов другого пользователя.

## 5. Сервис досок
Хранит информацию о досках с карточками задач пользователей:
- предмет;
- заголовок;
- описание;
- дата сдачи задачи.

Выполняет функции:
- хранение, изменение и отдача досок пользователей;
- получение списка досок пользователя;
- проверка прав пользователя на чтение и редактирование досок другого пользователя.

# Требования по реализации со стороны заказчика

1. Сервисы запускаются изолированно друг от друга.
2. Требуется использовать сервис-ориенторованную архитектуру.
3. Отказ сервиса, реализующего некритичный функционал, не приводит к отказу системы в целом.
4. Необходимо реализовать клиент для взаимодествия с системой - одностраничное приложение для доступа из веб-браузера.
5. Взаимодествие с бэкендом системы реализуется через фронтенд сервис, другие сервисы изолированы от прямого доступа из внешней сети.

# Функциональные требования по подсистемам

## 1. Фронтенд-сервер:
- принимает запросы по протоколу HTTP;
- проксирует запросы к подсистемам по протоколу HTTP.

## 2. Сервис авторизации
- принимает запросы по протоколу HTTP; 
- выполняет валидацию входных данных;
- входные/выходные данные имеют формат JSON;
- поддерживается авторизация через социальную сеть VK;
- база данных, содержащая информацию о данных регистрации, должна находиться на этом же сервере (
доступ к СУБД осуществляется по протоколу TCP);
- резервирование базы данных должно производиться автоматически по расписанию.

## 3. Сервис профилей
- принимает запросы по протоколу HTTP; 
- выполняет валидацию входных данных;
- входные/выходные данные имеют формат JSON;
- доступ к СУБД осуществляется по протоколу TCP;
- резервирование базы данных должно производиться автоматически по расписанию;
- необходимо выполнить шардирование базы данных, ключ шардирования подобрать из условия наиболее равномерного разделения данных между серверами.

## 5. Сервис документов
- принимает запросы по протоколу HTTP;
- выполняет валидацию входных данных;
- аватары пользователей имеют формат JPEG;
- документы пользователей имеют формат Markdown.

## 6. Сервис досок
- принимает запросы по протоколу HTTP; 
- выполняет валидацию входных данных;
- входные/выходные данные имеют формат JPEG;
- доступ к СУБД осуществляется по протоколу TCP;
- резервирование базы данных должно производиться автоматически по расписанию;
- необходимо выполнить шардирование базы данных, ключ шардирования подобрать из условия наиболее равномерного разделения данных между серверами.

# Сценарий взаимодествия фронтенд-сервера с сервисами

1. На фронтенд-сервер приходит запрос по протоколу HTTP.
2. Фронтенд-сервер анализирует заголовки запроса на наличие токена авторизации. В случае, если токен найден, фронтенд-сервер выполняет запрос к сервису авторизации с целью проверки токена и получения идентификатора пользователя, от имени которого выполнен запрос. Сервис авторизации выбирается случайным образом. На запрос устанавливается максимальное время ожидания ответа (таймаут). Если запрос не успевает выполниться за данное время, запрос повторно отправляется к другому сервису авторизации. Так продолжается, пока ответ не будет получен от одного из сервисов. В случае недоступности всех сервисов пользователю возвращается ошибка.
3. В случае, если токен авторизации недействителен, пользователю возвращается ошибка.
4. Фронтенд-сервер выполняет запрос к выбранному на основании параметров запроса сервису, при этом, если запрос был авторизован, к заголовкам запроса добавляется идентификатор пользователя. Сервис выбирается случайным образом. На запрос устанавливается максимальное время ожидания ответа (таймаут). Если запрос не успевает выполниться за данное время, запрос повторно отправляется к другому сервису. Так продолжается, пока ответ не будет получен от одного из сервисов. В случае недоступности всех сервисов пользователю возвращается ошибка.

# Сценарий взаимодействия сервисов с СУБД

1. Севрис получает запрос от фронтенд-сервера.
2. Для обращения к СУБД сервис использует прокси, инкапсулирующий логику репликации и шардирования СУБД. Запросы на запись обрабатываются ведущим (master) сервером СУБД, запросы на чтение - ведомым (slave) сервером.
3. Запросы на чтение выполняются по очереди к ведомым серверам, пока ответ не будет получен от одного из них.
4. В случае недоступности ведущего сервера запрос на запись не может быть обработан и возвращается ошибка; в случае недоступности всех серверов не может быть обработан запрос на чтение и возвращается ошибка.
