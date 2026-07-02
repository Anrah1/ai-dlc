# Получение информации о сотруднике

**GET** `/management/employees/{id}`

Получение информации о сотруднике
**Описание метода:**
Метод предназначен для получения информации о конкретном сотруднике по его id
Метод: GET
Эндпоинт: /management/employees/{id}
**Строка запроса: **GET https:// ... /management/employees/1
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
| grade | + | object | planer.employees.grade | Грейд руководителя |
| leader | - | string |  | null значение |
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
| file | - | object | - |  |
| id | - | uuid | - | Универсальный уникальный идентификатор (uuid) файла  резюме в хранилище |
| name | - | string | - | Название файла резюме |
| link | - | string | - | Ссылка на скачивание из хранилища |

| { / "id":1, / "lastName": "Иванов", / "firstName": "Иван", / "middleName": "Иванович", / "role": { / "id": 3, / "name": "Аналитик" / }, / "subrole": { / "id": 5, / "name": "Системный" / }, / "grade": "MIDDLE", / "leader": { / "id": 2, / "lastName": "Петров", / "firstName": "Петр", / "middleName": "Петрович", / "role": { / "id": 2, / "name": "Тимлид" / }, / "grade": "LEAD_EXPERT", / "leader": **null**, / "type": "INTERNAL", / "status": "ACTIVE" / }, / "birthDate": "1999-01-01", / "type": "INTERNAL", / "status": "ACTIVE", / "file": { / "id": "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11", / "name": "CV_Смирнов Д._2025-02-03T18:11:10.74573", / "link": "dfFzfdxdfxdgfxfg" / } / } |
| --- |

Ошибки:
404 Not Found

| { / "message": "Сотрудник с идентификатором '123' не найден." / } |
| --- |
