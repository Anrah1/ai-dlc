# Создание назначения

**POST** `/management/appointments`

Создание назначения
**Описание метода:**
Метод предназначен для создания нового назначения.
Валидация:
- Проверка заполнения обязательных полей: id, employeeId, roleId, grade, projectId, startDate, endDate, customers, condition, paymentDates (id, date), status, иначе вызывается ошибка 400.
- Проверка заполнения обязательных полей при отправке paymentDates: id, fromChargeCode, toChargeCode, type, иначе вызывается ошибка 400.
- Проверка существования id для сотрудника, проекта, роли, подроли, иначе вызывается ошибка 404.
- Проверка зависимости между ролью и подролью, иначе ошибка 409.
Метод: POST
Эндпоинт: /management/appointments
**Строка**** запроса****: **POST  /management/appointments

| **Параметр** | **Обязательность** | **Тип данных** | **Мэппинг на БД** | **Описание поля** |
| --- | --- | --- | --- | --- |
| employeeId | + | number / (формат: integer($int64)) | planer.appointments.employee_id | ID сотрудника |
| roleId | + | number / (формат: integer($int32)) | planer.appointments.role_id | Роль на проекте |
| subroleId | - | number / (формат: integer($int32)) | planer.appointments.subrole_id | Подроль |
| grade | + | string | planer.appointments.grade | Грейд |
| projectId | + | number / (формат: integer($int64)) | planer.appointments.project_id | Проект |
| startDate | + | string / (формат: date) | planer.appointments.start_date | Дата подключения |
| endDate | + | string / (формат: date) | planer.appointments.end_date | Дата отключения |
| responsibleForFeedback | - | string | planer.appointments.responsible_for_feedback | Ответственный за обратную связь |
| customers | + | string | planer.appointments.customers | Заказчики |
| partner | - | string | planer.appointments.partner | Партнер |
| ratePartner | - | number | planer.appointments.rate_partner | Ставка у партнера |
| condition | + | string | planer.appointments.condition | Условия |
| rateNoNds | - | number | planer.appointments.rate_no_nds | Ставка без НДС |
| percent | - | number | planer.appointments.percent | Проценты |
| **paymentDates** | - | array[object] |  |  |
| id | + | number / (формат: integer($int64)) | planer.payment_dates.id | ID даты оплаты (передается в запросе null) |
| date | + | string / (формат: date) | planer.payment_dates.date | Дата оплаты |
| comment | - | string | planer.appointments.comment | Комментарий |
| **chargeCodes** | - | array[object] |  |  |
| id | + | number / (формат: integer($int64)) | planer.charge_codes.id | ID ЧК ((передается в запросе null) |
| fromChargeCode | + | string | planer.charge_codes.from_charge_code | Условие по ЧК: ЧК откуда |
| toChargeCode | + | string | planer.charge_codes.to_charge_code | Условие по ЧК: ЧК куда |
| type | + | string<br>(формат: enum) | planer.charge_codes.type | Условие по ЧК: ЧК доход или расход |
| status | + | string / (формат: enum) | planer.appointments.status | Статус |

**Дополнительные сведения:**
Для объектов paymentDates мы не указываем id, либо указываем null, так как он автогенерируется базой при сохранении.

| "paymentDates": [ / { // вариант 1 / "id": **null**, / "date": "2025-01-01" / }, / { // вариант 2 / "date": "2025-02-02" / } / ] |
| --- |

**Пример запроса:** POST /management/appointments

| { / "employeeId": 10, / "roleId": 2, / "subroleId": 1, / "grade": "MIDDLE", / "projectId": 10, / "startDate": "2024-12-01", / "endDate": "2025-02-25", / "customers": "Петров Петр (трайб POS)", / "responsibleForFeedback": "Иванова Мария", / "condition": "PROFITSHARING", / "rateNoNds": 1200, / "paymentDates": [ / { / "id": **null**, / "date": "2024-01-05" / }, / { / "id": **null**, / "date": "2024-02-05" / } / ], / "status": "ACTIVE", / "chargeCodes": [ / { / "id": **null**, / "fromChargeCode": "CRM_RSB_N_TELE2_TDSOS", / "toChargeCode": "INV_OCS_N_TELE2_TDSOS", / "type": "PROFIT" / }, / { / "id": **null**, / "fromChargeCode": "INV_OCS_N_TELE2_TDS", / "toChargeCode": "INV_OCS_N_TELE2_TDSOS", / "type": "EXPENSE" / } / ] / } |
| --- |

**Ответ:**

| **Параметр** | **Обязательность** | **Тип данных** | **Мэппинг на БД** | **Описание поля** |
| --- | --- | --- | --- | --- |
| id | + | number / (формат: integer($int64)) | planer.appointments.id | ID назначения |
| **employee** | + | object |  |  |
| id | + | number / (формат: integer($int64)) | planer.employees.id | ID сотрудника |
| lastName | + | string | planer.employees.last_name | Фамилия сотрудника |
| firstName | + | string | planer.employees.first_name | Имя сотрудника |
| middleName | - | string | planer.employees.middle_name | Отчество сотрудника |
| role | + | object |  |  |
| id | + | number / (формат: integer($int32)) | planer.roles.id | ID роли |
| name | + | string | planer.roles.name | Роль |
| subrole | - | object |  |  |
| id | + | number / (формат: integer($int32)) | planer.subroles.id | ID подроли |
| name | + | string | planer.subroles.name | Подроль |
| grade | + | string | planer.employees.grade | Грейд |
| **leader** | + | object |  |  |
| id | + | number / (формат: integer($int64)) | planer.employees.id | ID сотрудника |
| lastName | + | string | planer.employees.last_name | Фамилия сотрудника |
| firstName | + | string | planer.employees.first_name | Имя сотрудника |
| middleName | - | string | planer.employees.middle_name | Отчество сотрудника |
| role | + | object |  |  |
| id | + | number / (формат: integer($int32)) | planer.roles.id | ID роли |
| name | + | string | planer.roles.name | Роль |
| subrole | - | object |  |  |
| id | + | number / (формат: integer($int32)) | planer.subroles.id | ID подроли |
| name | + | string | planer.subroles.name | Подроль |
| grade | + | string | planer.employees.grade | Грейд |
| leader | - | object |  |  |
| birthDate | - | string / (формат: date) | planer.employees.birth_date | Дата рождения |
| tgRef | - | string | planer.employees.tg_ref | Telegram менеджера руководителя |
| externalManager | - | string | planer.employees.external_manager | Руководитель внешнего сотрудника |
| type | + | string / (формат: enum) | planer.employees.type | Тип сотрудника(внешний/внутренний) |
| status | + | string / (формат: enum) | planer.employees.status | Статус |
| comment | - | string / (формат: date) | planer.employees.comment | Комментарий |
| birthDate | - | string | planer.employees.birth_date | Дата рождения |
| externalManager | - | string | planer.employees.external_manager | Руководитель внешнего сотрудника |
| tgRef | - | string | planer.employees.tg_ref | Telegram менеджера руководителя |
| type | + | string / (формат: enum) | planer.employees.type | Тип сотрудника(внешний/внутренний) |
| status | + | string / (формат: enum) | planer.employees.status | Статус |
| comment | - | string | planer.employees.comment | Комментарий |
| role | + | object |  |  |
| id | + | number / (формат: integer($int32)) | planer.roles.id | ID роли |
| name | + | string | planer.roles.name | Роль |
| subrole | - | object |  |  |
| id | + | number / (формат: integer($int32)) | planer.subroles.id | ID подроли |
| name | + | string | planer.subroles.name | Подроль |
| **project** | + | object |  |  |
| id | + | number / (формат: integer($int64)) | planer.projects.id | ID проекта |
| name | + | string | planer.projects.name | Название проекта |
| manager | - | object |  | Менеджер проекта |
| type | + | string / (формат: enum) | planer.projects.type | Тип проекта(внешний/внутренний) |
| chargeCode | - | string | planer.projects.charge_code | Код проекта (ЧК) |
| status | + | string / (формат: enum) | planer.projects.status | Статус |
| comment | - | string | planer.projects.comment | Комментарий |
| startDate | + | string / (формат: date) | planer.appointments.start_date | Дата подключения |
| endDate | + | string / (формат: date) | planer.appointments.end_date | Дата отключения |
| customers | + | string | planer.appointments.customers | Заказчики |
| responsibleForFeedback | - | string | planer.appointments.responsible_for_feedback | Ответственный за обратную связь |
| partner | - | string | planer.appointments.partner | Партнер |
| ratePartner | - | number | planer.appointments.rate_partner | Ставка у партнера |
| condition | + | string | planer.appointments.condition | Условия |
| rateNoNds | - | number | planer.appointments.rate_no_nds | Ставка без НДС |
| percent | - | number | planer.appointments.percent | Проценты |
| **paymentDates** | - | array[object] |  |  |
| id | - | number / (формат: integer($int64)) | planer.payment_dates.id | ID даты оплаты |
| date | - | string / (формат: date) | planer.payment_dates.date | Дата оплаты |
| comment | - | string | planer.appointments.comment | Комментарий |
| **chargeCodes** | - | array[object] |  |  |
| id | - | number / (формат: integer($int64)) | planer.charge_codes.id | ID ЧК |
| fromChargeCode | - | string | planer.charge_codes.from_charge_code | Условие по ЧК: ЧК откуда |
| toChargeCode | - | string | planer.charge_codes.to_charge_code | Условие по ЧК: ЧК куда |
| type | - | string / (формат: enum) | planer.charge_codes.type | Условие по ЧК: ЧК доход или расход |
| status | + | string / (формат: enum) | planer.appointments.status | Статус назначения |

**Пример успешного ответа:**
201 Created: Назначение успешно создано.

| { / "id": 12, / "employee": { / "id": 10, / "lastName": "Иванов", / "firstName": "Иван", / "middleName": "Иванович", / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Системный" / }, / "leader": { / "id": 2, / "lastName": "Петров", / "firstName": "Иван", / "middleName": "Петрович", / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": **null**, / "grade": "SENIOR", / "birthDate": "1999-07-07", / "leader": **null**, / "externalManager": **null**, / "tgRef": **null**, / "type": "INTERNAL", / "status": "ACTIVE", / "comment": **null** / }, / "birthDate": "1999-01-01", / "externalManager": **null**, / "tgRef": **null**, / "type": "INTERNAL", / "status": "ACTIVE", / "comment": **null** / }, / "project": { / "id": 10, / "name": "Siebel", / "manager": **null**, / "type": "INTERNAL", / "chargeCode": "CRM_123123123", / "status": "ACTIVE", / "comment": "" / }, / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Системный" / }, / "grade": "MIDDLE", / "startDate": "2024-12-01", / "endDate": "2025-02-25", / "customers": "Петров Петр (трайб POS)", / "responsibleForFeedback": "Иванова Мария", / "condition": "PROFITSHARING", / "paymentDates": [ / { / "id": 1, / "date": "2024-01-05" / }, / { / "id": 2, / "date": "2024-02-05" / } / ], / "partner": **null**, / "ratePartner": **null**, / "rateNoNds": "1200.0", / "percent": **null**, / "comment": "", / "status": "ACTIVE", / "chargeCodes": [ / { / "id": 11, / "fromChargeCode": "CRM_RSB_N_TELE2_TDSOS", / "toChargeCode": "INV_OCS_N_TELE2_TDSOS", / "type": "PROFIT" / }, / { / "id": 12, / "fromChargeCode": "INV_OCS_N_TELE2_TDS", / "toChargeCode": "INV_OCS_N_TELE2_TDSOS", / "type": "EXPENSE" / } / ] / } |
| --- |

**Ошибки:**
400 Bad Request: Некорректные данные запроса

| { / "employeeId": "Поле 'сотрудник' не может быть пустым.", / "roleId": "Поле 'роль' не может быть пустым.", / "grade": "Поле 'грейд' не может быть пустым.", / "projectId": "Поле 'проект' не может быть пустым.", / "startDate": "Поле 'дата подключения' не может быть пустой.", / "endDate": "Поле 'дата отключения' не может быть пустой.", / "customers": "Поле 'заказчики' не может быть пустым.", / "condition": "Поле 'условия' не может быть пустым.", / "status": "Поле 'статус' не может быть пустым." / } |
| --- |

404 Not Found: Проект/сотрудник не найден.

| { / "project": "Проект с идентификатором 'id' не найден.", / "employee": "Сотрудник с идентификатором 'id' не найден.", / "role": "Роль с идентификатором 'id' не найдена.", / "subrole": "Подроль с идентификатором 'id' не найдена." / } |
| --- |

409 Conflict: Для роли не существует указанной подроли.

| { / "message": "Для указанной роли не существует подроли с идентификатором 'id'." / } |
| --- |
