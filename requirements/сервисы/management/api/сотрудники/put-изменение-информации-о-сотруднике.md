# Изменение информации о сотруднике

**PUT** `/management/employees/{id}`

Изменение информации о сотруднике
**Описание метода:**
Метод предназначен для обновления информации о сотруднике по его id.
**Логика выполнения метода:**
После получения данных выполняется:
- Проверка заполнения обязательных полей: id, lastName, firstName, roleId, grade, type, status
- Проверка наличия в БД указанных параметров roleId, subroleId:
Валидация roleId, subroleId
При получении запроса сервис проводит валидацию данных параметров roleId, subroleId (если указан):
если роль, подроль (если указана) с указанным id найдены, то проверка пройдена успешно
иначе, сервис выводит ошибку
- Проверка зависимости параметра subroleId от параметра roleId:
Валидация зависимости subroleId от roleId
При получении запроса сервис проводит валидацию зависимости параметра subroleId от параметра roleId:
если подроль с указанным id найдена для указанного id роли, то проверка пройдена успешно
иначе, сервис выводит ошибку
- Проверка наличия сотрудника с указанным id для параметра leaderId:
Валидация leaderId
При получении запроса сервис проводит валидацию данных параметра leaderId:
если сотрудник с указанным id найден, то проверка пройдена успешно
иначе, сервис выводит ошибку
- Проверка наличия активного назначения у сотрудника при изменении статуса на "FIRED":
Валидация при увольнении
При получении запроса на изменение параметра status на "FIRED" сервис проводит валидацию на наличие у сотрудника активного назначения:
если назначения со статусом "ACTIVE" отсутствуют, то проверка пройдена успешно
иначе, сервис выводит ошибку
- Проверка корректности данных параметра managerContact:
Валидация managerContact
При получении запроса сервис проводит валидацию данных параметра managerContact:
разрешен ввод в форматах "@tgname1", "+00000000000" или "80000000000"
если первый символ @, то ограничение 5-32 символов (только английские буквы, цифры и символ "_");
если первый символ +, то ограничение 10-15 символов (только цифры);
если первый символ 8, то ограничение 10-14 символов (только цифры);
иначе, сервис выводит ошибку
- Проверка наличия циклической зависимости между id и параметром leaderId
Валидация циклической зависимости
При получении запроса сервис проводит валидацию на наличие циклической зависимости между id сотрудника и параметром leaderId:
если в цепочке leaderId не найдено совпадений с id сотрудника, то проверка пройдена успешно
иначе, сервис выводит ошибку
После успешной валидации выполняется сбор информации об изменении (аудит). Происходит сравнение старой записи с новыми полученными данными. В аудит входит:
Идентификатор изменяемой записи (employee_id);
Название изменяемых полей (changed_field);
Тип изменяемых полей (field_data_type);
Старые и новые значения данных (previous_value и new_value);
Временная метка изменения (updated_at);
ФИ пользователя, внесшего изменения (updated_by).
Далее аудит отправляется в БД: схему history, таблицу employees (подробнее в описании ).
3. Новые значения записи (полученные данные) обновляются в БД: схеме planer, таблице employees.
Метод: PUT
Эндпоинт: /management/employees/{id}
**Строка запроса: **PUT https:// … /management/employees/3
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

| { / "lastName": "Сергеев", / "firstName": "Сергей", / "middleName": "Сергеевич", / "roleId": 3, / "subroleId": 5, / "grade": "SENIOR", / "leaderId": 2, / "birthDate": "1999-01-01", / "comment": "Комментарий", / "type": "INTERNAL", / "status": "ACTIVE", / "fileUuid": "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11" / } |
| --- |

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
| id | + | number / (формат: integer($int32)) | planer.subroles.id | Идентификатор подроли |
| name | + | string | planer.subroles.name | Наименование подроли |
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

| { / "id":3, / "lastName": "Сергеев", / "firstName": "Сергей", / "middleName": "Сергеевич", / "role": { / "id": 3, / "name": "Аналитик" / }, / "subrole": { / "id": 5, / "name": "Системный" / }, / "grade": "SENIOR", / "leader": { / "id": 2, / "lastName": "Петров", / "firstName": "Петр", / "middleName": "Петрович", / "role": { / "id": 2, / "name": "Тимлид" / }, / "grade": "LEAD_EXPERT", / "leader": **null**, / "type": "INTERNAL", / "status": "ACTIVE" / }, / "birthDate": "1999-01-01", / "comment": "Комментарий", / "type": "INTERNAL", / "status": "ACTIVE", / "file": { / "id": "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11", / "name": "CV_Смирнов Д._2025-02-03T18:11:10.74573", / "link": "dfFzfdxdfxdgfxfg" / } / } |
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

Code Block 1 Ошибка валидации зависимости subroleId от roleId

| Пример ошибки если сотрудник ссылается сам на себя: / { / "message": "Обнаружена циклическая зависимость между сотрудником и руководителем. / Иванов Иван Иванович -> Иванов Иван Иванович" / } / Пример ошибки если сотрудников < 4: / { / "message": "Обнаружена циклическая зависимость между сотрудником и руководителем. / Иванов Иван Иванович -> Петров Петр Петрович -> Иванов Иван Иванович" / } / Пример ошибки если сотрудников >= 4: / { / "message": "Обнаружена циклическая зависимость между сотрудником и руководителем. / Иванов Иван Иванович -> Сергеев Сергей Сергеевич -> ... -> Петров Петр Петрович -> Иванов Иван Иванович" / } |
| --- |

Code Block 2 Ошибка валидации циклической зависимости
422 Unprocessable Entity

| { / "message": "Сотрудник 'Фамилия Имя Отчество' не может быть уволен, имеется активное назначение." / } |
| --- |

###### Методы для работы с назначениями
