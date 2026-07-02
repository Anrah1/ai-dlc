# Получение списка всех проектов

**GET** `/management/projects`

Получение списка всех проектов
**Описание метода:**
Метод предназначен для получения списка всех проектов
Метод: GET
Эндпоинт: https://management/projects
**Строка**** запроса****: **GET  https://management/projects
**Тело запроса: **отсутствует
**Ответ:**

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
| leader | number / (формат: integer($int64)) | - | Руководитель менеджера | planer.employees.leader_id |
| externalManager | string | - | Внешний менеджер (для внешних сотрудников) | planer.employees.external_manager |
| managerContact | string | - | Контакт внешнего менеджера | planer.employees.manager_contact |
| birthDate | string / (формат: date) | - | Дата рождения менеджера | planer.employees.birth_date |
| comment | string | - | Комментарий к карточке менеджера | planer.employees.comment |
| type | string / (формат: enum) | + | Тип сотрудника у менеджера<br>enum (Внутренний/Внешний) | planer.employees.type |
| status | string / (формат: enum) | + | Статус менеджера | planer.employees.status |
| type | string / (формат: enum) | + | Тип проекта enum (Внутренний/Внешний) | projects.type |
| status | string / (формат: enum) | + | Статус проекта из списка (enum: Активный, Завершен) | planer.projects.status |
| chargeCode | string | - | Список Кодов проекта (ЧК). В БД хранится  строкой с разделителем ";" | planer.projects.charge_code |
| comment | string | - | Комментарий к проекту | planer.projects.comment |
| createdAt | string / (формат: date-time) | + | Дата создания | planer.projects.created_at |
| updatedAt | string / (формат: date-time) | + | Дата обновления | planer.projects.updated_at |

**Пример успешного ответа**
200 ОК
**Пример тела**** ответа****:**

| [ / { / "id": 12345, / "name": "Планер", / "manager": { / "id": 11, / "lastName": "Петров", / "firstName": "Петр", / "middleName": "Петрович", / "role": "MANAGER", / "grade": "LEAD_EXPERT", / "leader": **null**, / "externalManager": "string", / "managerContact": "string", / "birthDate": "string", / "comment": "string", / "type": "INTERNAL", / "status": "ACTIVE" / }, / "type": "INTERNAL", / "chargeCode": "CRM_123123123", / "status": "ACTIVE", / "comment": "комментарий", / "createdAt": "2024-11-10T13:11:10.74573", / "updatedAt": "2025-02-03T13:11:10.74573" / } / ] |
| --- |

**Примеры ответов в случае ошибки**
204 No Content
*Запрос выполнен успешно, но в ответе отсутствует контент. (может произойти, если проектов нет)
404 Not Found: указан неверный url

| { / "timestamp": "2024-12-19T10:04:37.345+00:00", / "status": "404", / "error": "Not Found", / "path": "/management/projects1" / } |
| --- |
