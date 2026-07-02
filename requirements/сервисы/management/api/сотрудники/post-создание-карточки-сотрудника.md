# Создание карточки сотрудника

**POST** `/management/employees`

Создание карточки сотрудника
**Описание метода:**
Метод предназначен для создания новой записи о сотруднике
Метод: POST
Эндпоинт: /management/employees
**Валидации:**
- Проверка заполнения обязательных полей: lastName, firstName, roleId, grade, type, status
Валидация roleId, subroleId
При получении запроса сервис проводит валидацию данных параметров roleId, subroleId (если указан):
если роль, подроль (если указана) с указанным id найдены, то проверка пройдена успешно
иначе, сервис выводит ошибку
Валидация зависимости subroleId от roleId
При получении запроса сервис проводит валидацию зависимости параметра subroleId от параметра roleId:
если подроль с указанным id найдена для указанного id роли, то проверка пройдена успешно
иначе, сервис выводит ошибку
Валидация leaderId
При получении запроса сервис проводит валидацию данных параметра leaderId:
если сотрудник с указанным id найден, то проверка пройдена успешно
иначе, сервис выводит ошибку
Валидация managerContact
При получении запроса сервис проводит валидацию данных параметра managerContact:
разрешен ввод в форматах "@tgname1", "+00000000000" или "80000000000"
если первый символ @, то ограничение 5-32 символов (только английские буквы, цифры и символ "_");
если первый символ +, то ограничение 10-15 символов (только цифры);
если первый символ 8, то ограничение 10-14 символов (только цифры);
иначе, сервис выводит ошибку
**С****трока запроса: **POST https:// … /management/employees
**Тело запроса:**

| Название параметра | Обязательность | Тип данных | Мэппинг на БД | Описание |
| --- | --- | --- | --- | --- |
| lastName | + | string | planer.employees.last_name | Фамилия |
| firstName | + | string | planer.employees.first_name | Имя |
| middleName | - | string | planer.employees.middle_name | Отчество |
| roleId | + | number / (формат: integer($int32)) | planer.employees.role_id | Роль |
| subroleId | - | number / (формат: integer($int32)) | planer.employees.subrole_id | Подроль |
| grade | + | string | planer.employees.grade | Грейд |
| leaderId | - | number / (формат: integer($int64)) | planer.employees.leader_id | Идентификатор руководителя |
| externalManager | - | string | planer.employees.external_manager | Внешний менеджер |
| managerContact | - | string | planer.employees.manager_contact | Контакт менеджера |
| birthDate | - | string / (формат: date) | planer.employees.birth_date | Дата рождения в формате YYYY-MM-DD |
| comment | - | string | planer.employees.comment | Комментарий |
| type | + | string / (формат: enum) | planer.employees.type | Тип сотрудника |
| status | + | string / (формат: enum) | planer.employees.status | Статус |
| fileUuid | - | uuid | planer.employees.file_uuid | Универсальный уникальный идентификатор (uuid) файла резюме в хранилище |

| { / "lastName": "Сергеев", / "firstName": "Сергей", / "middleName": "Сергеевич", / "roleId": 3, / "subroleId": 5, / "grade": "SENIOR", / "leaderId": 2, / "type": "INTERNAL", / "status": "ACTIVE", / "fileUuid": "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11" / } |
| --- |

**Примеры ответов:**
Успешный ответ:
201 Created: Карточка сотрудника успешно создана

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
| grade | + | string | planer.employees.grade_id | Грейд |
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
| id | - | uuid | - | Универсальный уникальный идентификатор (uuid) файла резюме в хранилище |
| name | - | string | - | Название файла резюме |
| link | - | string | - | Ссылка на скачивание из хранилища |

| { / "id":3, / "lastName": "Сергеев", / "firstName": "Сергей", / "middleName": "Сергеевич", / "role": { / "id": 3, / "name": "Аналитик" / }, / "subrole": { / "id": 5, / "name": "Системный" / }, / "grade": "SENIOR", / "leader": { / "id": 2, / "lastName": "Петров", / "firstName": "Петр", / "middleName": "Петрович", / "role": { / "id": 2, / "name": "Тимлид" / }, / "grade": "LEAD_EXPERT", / "leader": **null**, / "type": "INTERNAL", / "status": "ACTIVE" / }, / "type": "INTERNAL", / "status": "ACTIVE", / "file": { / "id": "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11", / "name": "CV_Смирнов Д._2025-02-03T18:11:10.74573", / "link": "dfFzfdxdfxdgfxfg" / } / } |
| --- |

Ошибки:
400 Bad Request

| { / "message": "Неверный формат контактной информации.; Поле 'фамилия' не может быть пустым.; Поле 'имя' не может быть пустым." / } |
| --- |

404 Not Found

| { / "message": "Сотрудник с идентификатором '123' не найден." / } |
| --- |

| { / "message": "Роль с идентификатором '123' не найдена." / } |
| --- |

409 Conflict

| { / "message": "Для указанной роли не существует подроли с идентификатором '5'." / } |
| --- |
