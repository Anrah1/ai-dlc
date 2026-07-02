# Создание вакансии

**POST** `/management/vacancies`

Описание
**Описание метода:**
Метод предназначен для создания новой вакансии
Валидации:
Проверка заполнения обязательных полей.
Проверка существования id для сотрудника, проекта, роли, подроли, иначе вызывается ошибка 404.
Проверка зависимости между ролью и подролью.
Метод: POST
Эндпоинт: https://management/vacancies
**Строка** **запроса****:** POST  https://management/vacancies

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| roleId | number / (формат: integer($int32)) | + | Идентификатор роли | planer.vacancies.role_id |
| subroleId | number / (формат: integer($int32)) | - | Идентификатор подроли | planer.vacancies.subrole_id |
| grade | string | + | Грейд(ы), разделитель ";". / Хранятся в строке через ; | planer.vacancies.grade |
| projectId | number / (формат: integer($int64)) | + | Идентификатор проекта | planer.vacancies.project_id |
| tribe | string | - | Команда/трайб | planer.vacancies.tribe |
| quantityOfEmployees | number / (формат: integer($int32)) | + | Число сотрудников (Количество требуемых сотрудников) | planer.vacancies.quantity_of_employees |
| periodOfAttraction | string | - | Срок привлечения | planer.vacancies.period_of_attraction |
| customers | string | - | Заказчики | planer.vacancies.customers |
| processesBy | array | + | Кто обрабатывает<br>Массив Id сотрудников |  |
| employeeId | number / (формат: integer($int64)) | + | Идентификатор сотрудника | planer.employees.id |
| tags | string | - | Теги/Метки |  |
| requirements | string | - | Требования | planer.vacancies.requirements |
| comment | string | - | Комментарий | planer.vacancies.comment |
| dateOfRequest | string / (формат: date-time) | + | Датаобращения и время открытия вакансии | planer.vacancies.date_of_request |
| status | string / (формат: enum) | + | Статус Enum (см. в  ) | planer.vacancies.status |
| searchSource | string | + | Источники поиска (в каких источниках лиды могут искать кандидатов) / Хранятся в строке разделитель ";" | planer.vacancies.search_source |
| isDirect | boolean | + | Прямой запрос (флаг, является ли запрос на вакансию прямым) | planer.vacancies.is_direct |
| resumePreparationDateTime | string / (формат: date-time) | - | Дата и время подготовки резюме | planer.vacancies.resume_preparation_date_time |
| location | string | + | Локация | planer.vacancies.location |
| vendorRate | string | - | Ставка для Вендора | planer.vacancies.vendor_rate |
| experience | string | - | Опыт (лет) | planer.vacancies.experience |
| urgency | string <br>(формат: enum) | - | Срочность | planer.vacancies.urgency |

| **Статус** / "status": "IN_PROGRESS"   - приходит с фронта |
| --- |

**Пример** **запроса****:**

| { / "roleId": 3, / "subroleId": 1, / "grade": "Senior; Lead/expert", / "projectId": 10, / "tribe": "Планшеты", / "quantityOfEmployees": 2, / "periodOfAttraction": "На квартал", / "customers": "Смирнов, smir@sm.ru", / "processesBy": [15, 20], / "tags": "ЦФТ; Camunda", / "requirements": "Микросервисы, Siebel, React, Rabbit, Kafka", / "comment": "Желательно из финтеха", / "dateOfRequest": "2024-04-13T08:30:00Z", / "status": "IN_PROGRESS", / "searchSource": "ПЦКС; Лига; Рынок", / "isDirect": **false**, / "resumePreparationDateTime": "2024-04-13T08:30:00Z", / "location": "СНГ", / "vendorRate": "50 000", / "experience": "3+", / "urgency": "Срочно" / } |
| --- |

**Ответ:**

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| id | number / (формат: integer($int64)) | + | Идентификатор вакансии | planer.vacancies.id |
| role | object | + | Роль |  |
| id | number / (формат: integer($int32)) | + | Идентификатор роли | planer.roles.id |
| name | string | + | Название роли | planer.roles.name |
| subrole | object | - | Подроль |  |
| id | number / (формат: integer($int32)) | - | Идентификатор подроли | planer.subroles.id |
| name | string | - | Название подроли | planer.suboles.name |
| grade | string | + | Грейд(ы), разделитель ";". / Хранятся в строке через ; | planer.vacancies.grades |
| project | object | + | Проект |  |
| id | number / (формат: integer($int64)) | + | Идентификатор проекта | planer.projects.id |
| name | string | + | Название проекта | planer.projects.name |
| tribe | string | - | Трайб/команда | planer.vacancies.tribe |
| quantityOfEmployees | number / (формат: integer($int32)) | + | Число сотрудников / (Количество требуемых сотрудников) | planer.vacancies.quantity_of_employees |
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
| isDirect | boolean | + | Прямой запрос (флаг, является ли запрос на вакансию прямым) | planer.vacancies.is_direct |
| resumePreparationDateTime | string / (формат: date-time) | - | Дата и время подготовки резюме | planer.vacancies.resume_preparation_date_time |
| location | string | + | Локация | planer.vacancies.location |
| vendorRate | string | - | Ставка для Вендора | planer.vacancies.vendor_rate |
| experience | string | - | Опыт (лет) | planer.vacancies.experience |
| urgency | string <br>(формат: enum) | - | Срочность | planer.vacancies.urgency |

**Пример успешного ответа**
201 Created: Вакансия успешно создана

| { / "id": 5, / "role": { / "id": 3, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Бизнес" / }, / "grade": "Senior; Lead/expert", / "project": { / "id": 10, / "name": "Проект А" / }, / "tribe": "Планшеты", / "quantityOfEmployees": 2, / "periodOfAttraction": "На квартал", / "customers": "Смирнов, smir@sm.ru", / "processesBy": [ / { / "id": 15, / "lastName": "Иванов", / "firstName": "Иван" / }, / { / "id": 20, / "lastName": "Петров", / "firstName": "Петр" / } / ], / "tags": "ЦФТ; Camunda", / "requirements": "Микросервисы, Siebel, React, Rabbit, Kafka", / "comment": "Желательно из финтеха", / "dateOfRequest": "2024-04-13T08:30:00Z", / "status": "IN_PROGRESS", / "searchSource": "ПЦКС; Лига; Рынок", / "isDirect": **false**, / "resumePreparationDateTime": "2024-04-13T08:30:00Z", / "location": "СНГ", / "vendorRate": "50 000", / "experience": "3+", / "urgency": "Срочно" / } |
| --- |

**Ошибки:**
400 Bad Request: Некорректные данные запроса

| {"message": "Поле <название атрибута> не может быть пустым.; Поле <название атрибута 2> не может быть пустым."} / Разделитель между ошибками ; / Валидно для обязательных атрибутов: Роль, Грейд, Проект,  Число сотрудников, Кто обрабатывает, Дата обращения, Статус, Источники поиска, Локация. |
| --- |

404 Not Found: Роль/проект/сотрудник не найден(а).

| { / "message": "Роль с идентификатором 'id' не найдена." / } / { / "message": "Проект с идентификатором 'id' не найден." / } / { / "message": "Сотрудник с идентификатором 'id' не найден." / } |
| --- |

409 Conflict: Для роли не существует указанной подроли.

| { / "message": "Для указанной роли не существует подроли с идентификатором 'id'." / } |
| --- |
