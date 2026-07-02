# Получение информации о назначении по его ID

**GET** `/management/appointments/{id}`

Получение информации о назначении по ID
**Описание метода:**
Метод возвращает информацию о конкретном назначении по его ID.
Метод: GET
Эндпоинт: /management/appointments/{id}
**Строка**** запроса****: **GET /management/appointments/{id}
**Пример запроса:** GET /management/appointments/12
**Ответ:**
Аналогично:
**Пример успешного ответа: **
200 ОК:  Данные отправлены.

| { / "id": 12, / "employee": { / "id": 10, / "lastName": "Иванов", / "firstName": "Иван", / "middleName": "Иванович", / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Системный" / }, / "leader": { / "id": 2, / "lastName": "Петров", / "firstName": "Иван", / "middleName": "Петрович", / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": **null**, / "grade": "SENIOR", / "birthDate": "1999-07-07", / "leader": **null**, / "externalManager": **null**, / "tgRef": **null**, / "type": "INTERNAL", / "status": "ACTIVE", / "comment": **null** / }, / "birthDate": "1999-01-01", / "externalManager": **null**, / "tgRef": **null**, / "type": "INTERNAL", / "status": "ACTIVE", / "comment": **null** / }, / "project": { / "id": 10, / "name": "Siebel", / "manager": **null**, / "type": "INTERNAL", / "chargeCode": "CRM_123123123", / "status": "ACTIVE", / "comment": **null** / }, / "role": { / "id": 2, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Системный" / }, / "grade": "MIDDLE", / "startDate": "2024-12-01", / "endDate": "2025-02-25", / "customers": "Петров Петр (трайб POS)", / "responsibleForFeedback": **null**, / "condition": "PROFITSHARING", / "paymentDates": [ / { / "id": 1, / "date": "2024-01-05" / }, / { / "id": 2, / "date": "2024-02-05" / } / ], / "partner": **null**, / "ratePartner": **null**, / "rateNoNds": 1200, / "percent": **null**, / "comment": **null**, / "status": "ACTIVE", / "chargeCodes": [ / { / "id": 11, / "fromChargeCode": "CRM_RSB_N_TELE2_TDSOS", / "toChargeCode": "INV_OCS_N_TELE2_TDSOS", / "type": "PROFIT" / }, / { / "id": 12, / "fromChargeCode": "INV_OCS_N_TELE2_TDS", / "toChargeCode": "INV_OCS_N_TELE2_TDSOS", / "type": "EXPENSE" / } / ] / } |
| --- |

**Ошибки:**
404 Not Found: Назначение не найдено.

| { / "message": "Назначение с идентификатором 'id' не найдено." / } |
| --- |
