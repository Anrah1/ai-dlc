# Получение информации о назначениях

**GET** `/management/appointments`

Получение информации о назначениях
**Описание метода:**
Метод возвращает информацию о всех назначениях.
Метод: GET
Эндпоинт: /management/appointments
**Строка**** запроса****: **GET /management/appointments
**Ответ:**
Массив из: . К этому добавляются поля:

| **Параметр** | **Обязательность** | **Тип данных** | **Мэппинг на БД** | **Описание поля** |
| --- | --- | --- | --- | --- |
| createdAt | + | string | planer.appointments.created_at | Дата создания |
| updatedAt | + | string | planer.appointments.updated_at | Дата обновления |

**Пример успешного ответа: **
200 ОК:  Данные отправлены.

| [ / { / "id": 12, / "employee": { / "id": 10, / "lastName": "Иванов", / "firstName": "Иван", / "middleName": "Иванович", / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Системный" / }, / "grade": "MIDDLE", / "leader": { / "id": 2, / "lastName": "Петров", / "firstName": "Иван", / "middleName": "Петрович", / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": **null**, / "grade": "SENIOR", / "birthDate": "1999-07-07", / "leader": **null**, / "externalManager": **null**, / "tgRef": **null**, / "type": "INTERNAL", / "status": "ACTIVE", / "comment": **null** / }, / "birthDate": "1999-01-01", / "externalManager": **null**, / "tgRef": **null**, / "type": "INTERNAL", / "status": "ACTIVE", / "comment": **null** / }, / "project": { / "id": 10, / "name": "Siebel", / "manager": **null**, / "type": "INTERNAL", / "chargeCode": "CRM_123123123", / "status": "ACTIVE", / "comment": **null** / }, / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Системный" / }, / "grade": "MIDDLE", / "startDate": "2024-12-01", / "endDate": "2025-02-25", / "customers": "Петров Петр (трайб POS)", / "responsibleForFeedback": **null**, / "condition": "PROFITSHARING", / "paymentDates": [ / { / "id": 1, / "date": "2024-01-05" / }, / { / "id": 2, / "date": "2024-02-05" / } / ], / "partner": **null**, / "ratePartner": **null**, / "rateNoNds": 1200, / "percent": **null**, / "comment": **null**, / "status": "ACTIVE", / "chargeCodes": [ / { / "id": 11, / "fromChargeCode": "CRM_RSB_N_TELE2_TDSOS", / "toChargeCode": "INV_OCS_N_TELE2_TDSOS", / "type": "PROFIT" / }, / { / "id": 12, / "fromChargeCode": "INV_OCS_N_TELE2_TDS", / "toChargeCode": "INV_OCS_N_TELE2_TDSOS", / "type": "EXPENSE" / } / ], / "createdAt": "2024-11-10T13:11:10.74573", / "updatedAt": "2025-02-03T13:11:10.74573" / }, / { / "id": 13, / "employee": { / "id": 20, / "lastName": "Петрова", / "firstName": "Анна", / "middleName": "Ивановна", / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Системный" / }, / "grade": "MIDDLE", / "leader": { / "id": 2, / "lastName": "Петров", / "firstName": "Иван", / "middleName": "Петрович", / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": { / "id": 3, / "name": "Fullstack" / }, / "grade": "SENIOR", / "birthDate": "1999-07-07", / "leader": **null**, / "externalManager": **null**, / "tgRef": **null**, / "type": "INTERNAL", / "status": "ACTIVE", / "comment": **null** / }, / "birthDate": "1997-04-07", / "externalManager": **null**, / "tgRef": **null**, / "type": "INTERNAL", / "status": "ACTIVE", / "comment": **null** / }, / "project": { / "id": 10, / "name": "Siebel", / "manager": **null**, / "type": "INTERNAL", / "chargeCode": "CRM_123123123", / "status": "ACTIVE", / "comment": **null** / }, / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Системный" / }, / "grade": "MIDDLE", / "startDate": "2024-12-01", / "endDate": "2025-02-25", / "customers": "Петров Петр (трайб POS)", / "responsibleForFeedback": **null**, / "condition": "PROFITSHARING", / "paymentDates": [ / { / "id": 1, / "date": "2024-01-05" / }, / { / "id": 2, / "date": "2024-02-05" / } / ], / "partner": **null**, / "ratePartner": **null**, / "rateNoNds": 1200, / "percent": **null**, / "comment": **null**, / "status": "ACTIVE", / "createdAt": "2024-11-10T13:11:10.74573", / "updatedAt": "2025-02-03T13:11:10.74573" / } / ] |
| --- |

**Ошибки:**
400 Bad Request: Некорректные данные запроса

| { / "timestamp": "2024-12-13T08:25:02.744+00:00", / "status": 400, / "error": "Bad Request", / "path": "/management/appointments" / } |
| --- |

204 No Content: Запрос выполнен успешно, но в ответе отсутствует контент.

| { / } |
| --- |
