# Ершов Олег
## Используемая технология
Postgre SQL
## Функциональные требования
* Авторизация пользователя.
* Управление пользователями (CRUD).
* Система ролей.
* Журналирование  действий пользователя.
## Список таблиц

### Клиенты
* Описание
  + Таблица информации о зарегистрированных клиентах
* Поля
  + client_id (Primary Key, INT, Auto-increment) - уникальный идентификатор клиента
  + account_id (Foreign Key, INT) - заказ 
  + first_name (VARCHAR(50)) - имя клиента
  + last_name (VARCHAR(50)) - фамилия клиента
  + email (VARCHAR(319)) - электронная почта клиента
  + phone_number (VARCHAR(20)) - номер телефона клиента
* Связи
  + один ко многим с таблицей кредитных карт
  + один ко многим с таблицей кредитов 
  + один ко многим с таблицей отзывов клиентов
### Работники
* Описание
  + Таблица информации работников
* Поля
  + worker_id (Primary Key, INT, Auto-increment) - уникальный идентификатор клиента
  + first_name (VARCHAR(50)) - имя студента
  + last_name (VARCHAR(50)) - фамилия студента
  + email (VARCHAR(319)) - электронная почта студента
  + phone_number (VARCHAR(20)) - номер телефона студента
* Связи
  + многие ко многим с таблицей должностей
  + многие ко многим с таблицей заказов
### Счёт 
*Описание
  Таблица для счёта клиента
*Поля
  +Account ID (Primary Key, INT, Auto-increment) - уникальный идентификатор счёта
  +Customer ID (foreign key) - ссылка на клиента банка
  +Тип счёта (сберегатеьный, кредит и т.д) (VARCHAR(20))
  +Баланс на счёте (Float)
  +Статус счёта (открыт, закрыт,заморожен)(VARCHAR(20)
*Связи
  + многие к одному с таблицей клиентов
  + 
### Траназкции
*Описание
  + Таблица переводов со счетов
*Поля
  + Transaction ID (Primary Key, INT, Auto-increment) - уникальный идентификатор перевода
  + Account ID (foreign key) - ключ для связи со счётом
  + Transaction date and time (Date) - время и дата переводов
  + Transaction type (e.g., deposit, withdrawal, transfer, payment) (VARCHAR(20))
  + Amount (INT)
  + Transaction status (e.g., completed, pending, canceled) (VARCHAR(20))
  + Description (VARCHAR(200))
*Связи
  + Многие к одному с таблицей счетов
### Кредит
* Описание
  + Таблица для кредитных данных
* Поля
  + Loan ID (Primary Key, INT, Auto-increment)
  + Customer ID (foreign key)
  + Loan type (e.g., personal, mortgage, auto) (VARCHAR(20))
  + Loan amount (FLOAT)
  + Interest rate (FLOAT)
  + Loan status (e.g., approved, pending, paid) (VARCHAR(20))
* Связи
  + многие к одному с таблицей пользователей
  + один ко многим с таблицей расписания оплат по кредиту
### Росписание оплат
* Описание
  + Таблица для списка дат оплаты по кредиту
* Поля
  + ID (Primary Key, INT, Auto-increment)
  + Credit id  (foreign key, integer)
  + Date (TIME)
* Связи
  + многие к одному с таблицей кредитов
### Должности
* Описание
  Таблица должностей
* Поля
  + Position ID
  + Staff ID (foreign key, for employees)
  + Title (VARCHAR(20))
  + Description (VARCHAR(200))
* Связи
  + один ко многим с таблицей работников
### Команда
* Описание
  + Таблица для хранения составов команд, если должность связана с айти, то команда работающая над проектом, если напрямую банковская работа, то отделение банка, в котором работает человек
* Поля
  + ID (Primary key, INT, Auto increment)
  + Title (VARCHAR (200) )
  + Stuff amount (smallint)
* Связи
  Многие ко многим с таблицей работников 
### Кредитная карточка
* Описание
  + Таблица данных о кредитной карте
* Поля
  + ID (Primary Key,INT) 
  + Customer ID (foreign key,INT)
  + Credit limit (FLOAT)
  + Current balance (FLOAT)
  + Creation date (Date)
  + PinCode (smallint)
  + CVV (smallint)
* Связи
  + многие к одному с клиентом банка
### Курс валют
* Описание
  Таблица курсов валют
* Поля
  + Currency pair (e.g., USD/EUR) (VARCHAR (10) )
  + Exchange rate (FLOAT)
  + Date and time of rate update (date)
* Связи
  нет, просто храним
### Тех поддержка
* Описание
  + Таблица для регулирования оказания тех поддержки
* Поля
  + ID (INT,Primary key, Auto increment4)
  + Customer ID (foreign key,INT)
  + Employee ID (foreign key, for assigned support staff,INT)
  + Issue description (VARCHAR (500) )
  + Ticket status (e.g., open, in progress, resolved) (VARCHAR (20) )
* Связи
  многие к одному с таблицей пользователей
  многие к одному с таблицей работников
