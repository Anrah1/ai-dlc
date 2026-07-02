# Редактирование назначения

**PUT** `/management/appointments/{id}`

Редактирование назначения
**Описание метода:**
Метод предназначен для редактирования назначения без создания новой версии или для завершения назначения (изменяется только статус).
**Логика обработки метода:**
После получения данных выполняется валидация:
- Проверка заполнения обязательных полей: id, employeeId, roleId, grade, projectId, startDate, endDate, customers, condition, paymentDates (id, date), status, иначе вызывается ошибка 400.
- Проверка заполнения обязательных полей при отправке paymentDates: id, fromChargeCode, toChargeCode, type, иначе вызывается ошибка 400.
- Проверка существования id для сотрудника, проекта, роли, подроли, иначе вызывается ошибка 404.
- Проверка зависимости между ролью и подролью, иначе ошибка 409.
После успешной валидации выполняется сбор информации об изменении. Происходит сравнение старой записи с новыми полученными данными. Формируется запись, в которую входит следующее:
Идентификатор изменяемой записи (appointment_id);
Название изменяемых полей (changed_field);
Тип изменяемых полей (field_data_type);
Старые и новые значения данных (previous_value и new_value);
Временная метка изменения (updated_at);
ФИ пользователя, внесшего изменения (updated_by).
Далее запись сохраняется в БД: схему history, таблицу appoinments (подробнее в описании ).
3. Новые значения записи (полученные данные) обновляются в БД: схеме planer, таблице appointments.
Метод: PUT
Эндпоинт: /management/appointments/{id}
**Строка**** запроса****:  **PUT /management/appointments/{id}

| **Параметр** | **Обязательность** | **Тип данных** | **Мэппинг на БД** | **Описание поля** |
| --- | --- | --- | --- | --- |
| id | + | number / (формат: integer($int64)) | planer.appointments.id | ID назначения<br>Path параметр |
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
| id | + | number / (формат: integer($int64)) | planer.payment_dates.id | ID даты оплаты |
| date | + | string / (формат: date) | planer.payment_dates.date | Дата оплаты |
| comment | - | string | planer.appointments.comment | Комментарий |
| **chargeCodes** | - | array[object] | Если меняем какое-то значение в ЧК, то передаем весь массив | Если меняем какое-то значение в ЧК, то передаем весь массив |
| id | - | number / (формат: integer($int64)) | planer.charge_codes.id | Условие по ЧК: ID |
| fromChargeCode | - | string | planer.charge_codes.from_charge_code | Условие по ЧК: ЧК откуда |
| toChargeCode | - | string | planer.charge_codes.to_charge_code | Условие по ЧК: ЧК куда |
| type | - | string<br>(формат: enum) | planer.charge_codes.type | Условие по ЧК: ЧК доход или расход |
| status | + | string / (формат: enum) | planer.appointments.status | Статус |

**Дополнительные сведения:**
При обновлении полей paymentDates у назначения мы передаем полный список объектов, который хотим получить в результате.
Пусть у нас поле paymentDates имеет следующий вид:

| "paymentDates": [ / { / "id": 1, / "date": "2024-02-01" / }, / { / "id": 2, / "date": "2024-02-02" / } / ] |
| --- |

**Кейс1**: обновили дату для paymentDate с id = 1, тогда в запросе на редактирование назначения поле (массив) будет выглядеть следующим образом:

| "paymentDates": [ / { / "id": 1, / "date": "2024-04-22" // какая-то новая дата / }, / { / "id": 2, / "date": "2024-02-02" / } / ] |
| --- |

При этом второй объект paymentDate мы не изменяли, но должны также передать его, иначе он удалится!
**Кейс2: **обновление назначения и создание (добавление) нового paymentDate,
Поле в запросе будет выглядеть так:

| "paymentDates": [ / { / "id": 1, / "date": "2024-04-22" / }, / { / "id": 2, / "date": "2024-02-02" / }, / { / "id": **null**, / "date": "2024-03-11" / } / ] |
| --- |

**Кейс3:** обновление назначения с удалением двух записей paymentDate. например мы удалили записи с id=1 и id=2, а из предыдущего примера, у нас осталась еще одна запись, пусть после ее добавления ей был назначен id=3.
Поле в запросе в таком случае будет выглядеть так:

| "paymentDates": [ / { / "id": 3, / "date": "2024-03-11" / } / ] |
| --- |

**Кейс4:** обновляем назначение и удаляем все paymentDates. Тогда поле в запросе

| "paymentDates": [ / //пустой массив / ] |
| --- |

**Пример запроса:** PUT /management/appointments/12

| { / "employeeId": 10, / "roleId": 3, / "subroleId": **null**, / "grade": "JUNIOR", / "projectId": 10, / "startDate": "2024-12-01", / "endDate": "2025-02-25", / "customers": "Петров Петр (трайб POS)", / "responsibleForFeedback": "Иванова Мария", / "condition": "PROFITSHARING", / "rateNoNds": 1200, / "paymentDates": [ / { / "id": 1, / "date": "2024-01-05" / }, / { / "id": 2, / "date": "2024-02-05" / } / ], / "status": "ACTIVE", / "chargeCodes": [ / { / "id": 11, / "fromChargeCode": "CRM_RSB_N_TELE2_TDSOS", / "toChargeCode": "INV_OCS_N_TELE2_TDSOS", / "type": "PROFIT" / }, / { / "id": 12, / "fromChargeCode": "INV_OCS_N_TELE2_TDS", / "toChargeCode": "INV_OCS_N_TELE2_TDSOS", / "type": "EXPENSE" / } / ] / } |
| --- |

**Ответ:**
Аналогично:
**Пример успешного ответа:**
200 ОК: Данные назначения успешно обновлены.

| { / "id": 12, / "employee": { / "id": 10, / "lastName": "Иванов", / "firstName": "Иван", / "middleName": "Иванович", / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Системный" / }, / "grade": "MIDDLE", / "leader": { / "id": 2, / "lastName": "Петров", / "firstName": "Иван", / "middleName": "Петрович", / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": **null**, / "grade": "SENIOR", / "birthDate": "1999-07-07", / "leader": **null**, / "externalManager": **null**, / "tgRef": **null**, / "type": "INTERNAL", / "status": "ACTIVE", / "comment": **null** / }, / "birthDate": "1999-01-01", / "externalManager": **null**, / "tgRef": **null**, / "type": "INTERNAL", / "status": "ACTIVE", / "comment": **null** / }, / "project": { / "id": 10, / "name": "Siebel", / "manager": **null**, / "type": "INTERNAL", / "chargeCode": "CRM_123123123", / "status": "ACTIVE", / "comment": **null** / }, / "role": { / "id": 3, / "name": "Архитектор" / }, / "subrole": **null**, / "grade": "JUNIOR", / "startDate": "2024-12-01", / "endDate": "2025-02-25", / "customers": "Петров Петр (трайб POS)", / "responsibleForFeedback": **null**, / "condition": "PROFITSHARING", / "paymentDates": [ / { / "id": 1, / "date": "2024-01-05" / }, / { / "id": 2, / "date": "2024-02-05" / } / ], / "partner": **null**, / "ratePartner": **null**, / "rateNoNds": 1200, / "percent": **null**, / "comment": **null**, / "status": "ACTIVE", / "chargeCodes": [ / { / "id": 11, / "fromChargeCode": "CRM_RSB_N_TELE2_TDSOS", / "toChargeCode": "INV_OCS_N_TELE2_TDSOS", / "type": "PROFIT" / }, / { / "id": 12, / "fromChargeCode": "INV_OCS_N_TELE2_TDS", / "toChargeCode": "INV_OCS_N_TELE2_TDSOS", / "type": "EXPENSE" / } / ] / } |
| --- |

**Ошибки:**
400 Bad Request: Некорректные данные запроса

| { / "employeeId": "Поле 'сотрудник' не может быть пустым.", / "roleId": "Поле 'роль' не может быть пустым.", / "grade": "Поле 'грейд' не может быть пустым.", / "projectId": "Поле 'проект' не может быть пустым.", / "startDate": "Поле 'дата подключения' не может быть пустой.", / "endDate": "Поле 'дата отключения' не может быть пустой.", / "customers": "Поле 'заказчики' не может быть пустым.", / "condition": "Поле 'условия' не может быть пустым.", / "status": "Поле 'статус' не может быть пустым." / } |
| --- |

404 Not Found: Назначение/проект/сотрудник не найден.

| { / "appointment": "Назначение с идентификатором 'id' не найдено.", / "project": "Проект с идентификатором 'id' не найден.", / "employee": "Сотрудник с идентификатором 'id' не найден.", / "role": "Роль с идентификатором 'id' не найдена.", / "subrole": "Подроль с идентификатором 'id' не найдена." / } |
| --- |

409 Conflict: Для роли не существует указанной подроли.

| { / "message": "Для указанной роли не существует подроли с идентификатором 'id'." / } |
| --- |
