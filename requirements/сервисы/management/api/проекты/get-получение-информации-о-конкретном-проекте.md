# Получение информации о конкретном проекте

**GET** `/management/projects`

Получение информации о конкретном проекте
**Описание метода:**
Метод предназначен для просмотра подробной информации о конкретном проекте
Метод: GET
Эндпоинт: https://management/projects
**Строка**** запроса****: **GET  https://management/projects/{id}
**Тело запроса: **Отсутствует
**Пример успешного ответа**
200 ОК

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| id | number / (формат: integer($int64)) | + | Идентификатор проекта | planer.projects.id |
| name | string | + | Название проекта | planer.projects.name |
| manager | object | + | объект менеджер |  |
| id | number / (формат: integer($int64)) | + | Идентификатор менеджера | planer.projects.manager_id |
| lastName | string | + | Фамилия менеджера | planer.employees.last_name |
| firstName | string | + | Имя менеджера | planer.employees.first_name |
| middleName | string | - | Отчество менеджера | planer.employees.middle_name |
| role | object | + | Роль сотрудника | planer.employees.role |
| id | number / (формат: integer($int32)) | + | Идентификатор роли |  |
| name | string | + | Название роли |  |
| subrole | object | - | Подроль сотрудника | planer.employees.subrole |
| id | number / (формат: integer($int32)) | - | Идентификатор подроли |  |
| name | string | - | Название подроли |  |
| grade | string | + | Грейд | planer.employees.grade |
| leaderId | number / (формат: integer($int64)) | - | Руководитель менеджера | planer.employees.leader_id |
| externalManager | string | - | Внешний менеджер (для внешних сотрудников) | planer.employees.external_manager |
| managerContact | string | - | Контакт внешнего менеджера | planer.employees.manager_contact |
| birthDate | string / (формат: date) | - | Дата рождения менеджера | planer.employees.birth_date |
| comment | string | - | Комментарий к карточке менеджера | planer.employees.comment |
| type | string / (формат: enum) | + | Тип сотрудника у менеджера<br>enum (Внутренний/Внешний) | planer.employees.type |
| status | string / (формат: enum) | + | Статус менеджера | planer.employees.status |
| type | string / (формат: enum) | + | Тип проекта enum (Внутренний/Внешний) | planer.projects.type |
| status | string / (формат: enum) | + | Статус проекта из списка (enum: Активный, Завершен) | planer.projects.status |
| chargeCode | string | - | Список Кодов проекта (ЧК). В БД хранится  строкой с разделителем ";" | planer.projects.charge_code |
| comment | string | - | Комментарий к проекту | planer.projects.comment |

**Тело ответа:**

| { / "id": 12345, / "name": "Планер", / "manager": { / "id": 11, / "lastName": "Петров", / "firstName": "Петр", / "middleName": "Петрович", / "role": { / "id": 1, / "name": "Менеджер" / }, / "subrole": **null**, / "grade": "LEAD_EXPERT", / "leader": **null**, / "externalManager": "string", / "managerContact": **null**, / "birthDate": "1987-01-01", / "birthDate": "string", / "comment": "string", / "type": "INTERNAL", / "status": "ACTIVE" / }, / "type": "INTERNAL", / "chargeCode": "CRM_123123123", / "status": "ACTIVE", / "comment": "комментарий" / } |
| --- |

**Примеры ответов в случае ошибки**
400 Bad Request: Некорректные данные запроса

| { / "timestamp": "2024-12-19T10:04:37.345+00:00", / "status": "400", / "error": "Bad Request", / "path": "/management/projects/100%D0%B2" / } |
| --- |

Code Block 3 400
404 Not Found: Проверьте, существует ли проект с указанным идентификатором в системе
*происходит, если проект с указанным идентификатором не существует.

| { / "message": "Проект с идентификатором '100' не найден." / } |
| --- |

Code Block 4 404
