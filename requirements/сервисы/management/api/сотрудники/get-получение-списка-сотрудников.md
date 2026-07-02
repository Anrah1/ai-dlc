# Получение списка сотрудников

**GET** `/management/employees`

Получение списка сотрудников
**Описание метода:**
Метод предназначен для получения списка всех сотрудников
Метод: GET
Эндпоинт: /management/employees
**Строка запроса: **GET https:// ... /management/employees
**Тело запроса:**
Отсутствует
**Примеры ответов:**
Успешный ответ:
200 OK

| Название параметра | Обязательность | Тип данных | Мэппинг на БД | Описание |
| --- | --- | --- | --- | --- |
| id | + | number / (формат: integer($int64)) | planer.employees.id | Идентификатор сотрудника |
| lastName | + | string | planer.employees.last_name | Фамилия |
| firstName | + | string | planer.employees.first_name | Имя |
| middleName | - | string | planer.employees.middle_name | Отчество |
| **role** | + | object |  | Роль |
| id | + | number / (формат: integer($int32)) | planer.roles.id | Идентификатор роли |
| name | + | string | planer.roles.name | Наименование роли |
| **subrole** | - | object |  | Подроль |
| id | - | number / (формат: integer($int32)) | planer.subroles.id | Идентификатор подроли |
| name | - | string | planer.suboles.name | Наименование подроли |
| grade | + | string | planer.employees.grade | Грейд |
| **leader** | - | object |  | Руководитель сотрудника |
| id | + | number / (формат: integer($int64)) | planer.employees.id | Идентификатор руководителя |
| lastName | + | string | planer.employees.last_name | Фамилия руководителя |
| firstName | + | string | planer.employees.first_name | Имя руководителя |
| middleName | - | string | planer.employees.middle_name | Отчество руководителя |
| **role** | + | object |  | Роль руководителя |
| id | + | number / (формат: integer($int32)) | planer.roles.id | Идентификатор роли |
| name | + | string | planer.roles.name | Наименование роли |
| **subrole** | - | object |  | Подроль руководителя |
| id | - | number / (формат: integer($int32)) | planer.subroles.id | Идентификатор подроли |
| name | - | string | planer.suboles.name | Наименование подроли |
| leader | - | object |  | null значение |
| externalManager | - | string | planer.employees.external_manager | Внешний менеджер руководителя |
| managerContact | - | string | planer.employees.manager_contact | Контакт менеджера руководителя |
| birthDate | - | string / (формат: date) | planer.employees.birth_date | Дата рождения руководителя в формате YYYY-MM-DD |
| comment | - | string | planer.employees.comment | Комментарий |
| type | + | string / (формат: enum) | planer.employees.type | Тип сотрудника |
| status | + | string / (формат: enum) | planer.employees.status | Статус |
| externalManager | - | string | planer.employees.external_manager | Внешний менеджер |
| managerContact | - | string | planer.employees.manager_contact | Контакт менеджера |
| birthDate | - | string / (формат: date) | planer.employees.birth_date | Дата рождения в формате YYYY-MM-DD |
| comment | - | string | planer.employees.comment | Комментарий |
| type | + | string / (формат: enum) | planer.employees.type | Тип сотрудника |
| status | + | string / (формат: enum) | planer.employees.status | Статус |
| isExistsAppointment | + | boolean |  | Наличие активного назначения |
| createdAt | + | string / (формат: date-time) | planer.employees.created_at | Дата создания сущности в формате YYYY-MM-DDThh:mm: |
| updatedAt | - | string / (формат: date-time) | planer.employees.updated_at | Дата обновления сущности в формате YYYY-MM-DDThh:mm: |

| { / [ / { / "id":1, / "lastName": "Иванов", / "firstName": "Иван", / "middleName": "Иванович", / "role": { / "id": 3, / "name": "Аналитик" / }, / "subrole": { / "id": 5, / "name": "Системный" / }, / "grade": "MIDDLE", / "leader": { / "id": 2, / "lastName": "Петров", / "firstName": "Петр", / "middleName": "Петрович", / "role": { / "id": 2, / "name": "Тимлид" / }, / "grade": "LEAD_EXPERT", / "leader": **null**, / "type": "INTERNAL", / "status": "ACTIVE" / }, / "type": "INTERNAL", / "status": "ACTIVE", / "isExistsAppointment": **true**, / "createdAt": "2025-02-03-T17:26:10.357869" / }, / { / "id":2, / "lastName": "Петров", / "firstName": "Петр", / "middleName": "Петрович", / "role": { / "id": 2, / "name": "Тимлид" / }, / "grade": "LEAD_EXPERT", / "type": "INTERNAL", / "status": "ACTIVE", / "isExistsAppointment": **false**, / "createdAt": "2024-01-30T10:22:30.873215", / "updatedAt": "2025-02-01T15:34:25.129863" / } / ] / } |
| --- |

204 No Content
