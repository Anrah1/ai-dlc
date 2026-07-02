# Получение списка всех вакансий

**GET** `/management/vacancies`

Описание
**Описание метода:**
Метод предназначен для получения списка всех вакансий.
Метод:  GET
Эндпоинт: https://management/vacancies
**Строка** **запроса****:** GET https://management/vacancies
**Пример запроса:** GET https://management/vacancies
**Ответ:**
Массив из объектов:

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| id | number / (формат: integer($int64)) | + | Идентификатор вакансии | planer.vacancies.id |
| role | object | + | Роль |  |
| id | number / (формат: integer($int32)) | + | Идентификатор роли | planer.roles.id |
| name | string | + | Название роли | planer.roles.name |
| subrole | object | - | Подроль |  |
| id | number / (формат: integer($int32)) | - | Идентификатор подроли | planer.subroles.id |
| name | string | - | Название подроли | planer.suboles.name |
| grade | string | + | Грейд(ы), разделитель ";" | planer.vacancies.grades |
| project | object | + | Проект |  |
| id | number / (формат: integer($int64)) | + | Идентификатор проекта | planer.projects.id |
| name | string | + | Название проекта | planer.projects.name |
| tribe | string | - | Трайб/команда | planer.vacancies.tribe |
| quantityOfEmployees | number / (формат: integer($int32)) | + | Количество требуемых сотрудников | planer.vacancies.quantity_of_employees |
| periodOfAttraction | string | - | Срок привлечения | planer.vacancies.period_of_attraction |
| customers | string | - | Заказчики | planer.vacancies.customers |
| processesBy | array[object] | + | Кто обрабатывает |  |
| id | number / (формат: integer($int64)) | + | Идентификатор сотрудника | planer.employees.id |
| lastName | string | + | Фамилия сотрудника | planer.employees.last_name |
| firstName | string | + | Имя сотрудника | planer.employees.first_name |
| tags | string | - | Теги/метки, разделитель ";" | planer.vacancies.tags |
| requirements | string | - | Требования | planer.vacancies.requirements |
| comment | string | - | Комментарий | planer.vacancies.comment |
| dateOfRequest | string / (формат: date) | + | Дата обращения | planer.vacancies.date_of_request |
| status | string / (формат: enum) | + | Статус | planer.vacancies.status |
| searchSource | string | + | Источники поиска (в каких источниках лиды могут искать кандидатов) / Хранятся в строке разделитель ";" | planer.vacancies.search_source |
| createdAt | string / (формат: date-time) | + | Дата создания | planer.vacancies.createdAt |
| updatedAt | string / (формат: date-time) | + | Дата обновления | planer.vacancies.updatedAt |
| isDirect | boolean | + | Прямой запрос (флаг, является ли запрос на вакансию прямым) | planer.vacancies.is_direct |
| location | string | + | Локация | planer.vacancies.location |
| vendorRate | string | - | Ставка для Вендора | planer.vacancies.vendor_rate |
| experience | string | - | Опыт (лет) | planer.vacancies.experience |
| urgency | string <br>(формат: enum) | - | Срочность | planer.vacancies.urgency |

**Пример успешного ответа:**
200 ОК: Данные вакансии отправлены.

| [ / { / "id": 7, / "role": { / "id": 3, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Бизнес" / }, / "grade": "Senior", / "project": { / "id": 10, / "name": "Проект А" / }, / "tribe": "Планшеты", / "quantityOfEmployees": 3, / "periodOfAttraction": "На квартал", / "customers": "Смиронов, smir@sm.ru", / "processesBy": [ / { / "id": 15, / "lastName": "Иванов", / "firstName": "Иван" / }, / { / "id": 20, / "lastName": "Петров", / "firstName": "Петр" / } / ], / "tags": "ЦФТ, Camunda", / "requirements": "Микросервисы, Siebel, React, Rabbit, Kafka", / "comment": "Желательно из финтеха", / "dateOfRequest": "2025-02-10", / "status": "IN_PROGRESS", / "createdAt": "2024-11-10T13:11:10.74573", / "updatedAt": "2025-02-03T13:11:10.74573", / "isDirect": **false**, / "location": "СНГ", / "vendorRate": "50 000", / "experience": "3+", / "urgency": "Срочно" / }, / { / "id": 8, / "role": { / "id": 3, / "name": "Аналитик" / }, / "subrole": { / "id": 2, / "name": "Системный" / }, / "grade": "Senior", / "project": { / "id": 10, / "name": "Проект А" / }, / "tribe": "Трайб POS", / "quantityOfEmployees": 1, / "periodOfAttraction": "6 месяцев", / "customers": "Смирнов, smir@sm.ru", / "processesBy": [ / { / "id": 18, / "lastName": "Петрова", / "firstName": "Мария" / }, / { / "id": 45, / "lastName": "Логунов", / "firstName": "Николай" / } / ], / "tags": "ЦФТ, Camunda", / "requirements": "Микросервисы, Kafka", / "dateOfRequest": "2025-02-13", / "status": "IN_PROGRESS", / "searchSource": "ПЦКС; Лига; Рынок", / "createdAt": "2024-12-20T14:14:10.74573", / "updatedAt": "2025-02-03T18:11:10.74573", / "isDirect": **true**, / "location": "Без ограничений" / } / ] |
| --- |

**Ошибки:**
204 No Content: Запрос выполнен успешно, но в ответе отсутствует контент.

| { / } |
| --- |

###### Методы работы с кандидатами
