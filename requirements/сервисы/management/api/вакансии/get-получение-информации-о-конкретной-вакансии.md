# Получение информации о конкретной вакансии

**GET** `/management/vacancies/{id}`

Описание
**Описание метода:**
Метод предназначен для получения информации о конкретной вакансии.
Метод:  GET
Эндпоинт: https://management/vacancies/{id}
**Строка** **запроса****:** GET https://management/vacancies/{id}
**Пример запроса:** GET https://management/vacancies/7
**Ответ:**

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
| dateOfRequest | string / (формат: date-time) | + | Датаобращения и время открытия вакансии | planer.vacancies.date_of_request |
| status | string / (формат: enum) | + | Статус | planer.vacancies.status |
| searchSource | string | + | Источники поиска (в каких источниках лиды могут искать кандидатов) / Хранятся в строке разделитель ";" | planer.vacancies.search_source |
| createdAt | string / (формат: date-time) | + | Дата создания | planer.vacancies.createdAt |
| updatedAt | string / (формат: date-time) | + | Дата обновления | planer.vacancies.updatedAt |
| isDirect | boolean | + | Прямой запрос (флаг, является ли запрос на вакансию прямым) | planer.vacancies.is_direct |
| resumePreparationDateTime | string / (формат: date-time) | + | Дата и время подготовки резюме | planer.vacancies.resume_preparation_date_time |
| location | string | + | Локация | planer.vacancies.location |
| vendorRate | string | - | Ставка для Вендора | planer.vacancies.vendor_rate |
| experience | string | - | Опыт (лет) | planer.vacancies.experience |
| urgency | string <br>(формат: enum) | - | Срочность | planer.vacancies.urgency |

**Пример успешного ответа:**
200 ОК: Данные вакансии отправлены.

| { / "id": 7, / "role": { / "id": 3, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Бизнес" / }, / "grade": "Senior", / "project": { / "id": 10, / "name": "Проект А" / }, / "tribe": "Планшеты", / "quantityOfEmployees": 3, / "periodOfAttraction": "На квартал", / "customers": "Смирнов, smir@sm.ru", / "processesBy": [ / { / "id": 15, / "lastName": "Иванов", / "firstName": "Иван" / }, / { / "id": 20, / "lastName": "Петров", / "firstName": "Петр" / } / ], / "tags": "ЦФТ, Camunda", / "requirements": "Микросервисы, Siebel, React, Rabbit, Kafka", / "comment": "Желательно из финтеха", / "dateOfRequest": "2025-02-26T14:24:13", / "resumePreparationDateTime": "2024-04-13T08:30:00Z", / "status": "IN_PROGRESS", / "searchSource": "ПЦКС; Лига; Рынок", / "createdAt": "2025-02-26T14:24:13", / "updatedAt": "2025-02-03T13:11:10.74573", / "isDirect": **false**, / "location": "СНГ", / "vendorRate": "50 000", / "experience": "3+", / "urgency": "Срочно" / } |
| --- |

**Ошибки:**
404 Not Found: Вакансия не найдена.

| { / "message": "Вакансия с идентификатором 'id' не найдена." / } |
| --- |
