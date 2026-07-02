# Получение истории изменений сотрудника

**GET** `/management/employees/{employeeId}/history`

Получение истории изменений сотрудника
**Описание метода:**
Метод предназначен для получения истории изменений конкретного сотрудника.
Метод: GET
Эндпоинт: /management/employees/{employeeId}/history
**Строка запроса: **GET /management/employees/{employeeId}/history
**Пример запроса:**  GET /management/employees/10/history
**Пример ответа:**
200 OK

| Название параметра | Обязательность | Тип данных | Мэппинг на БД | Описание |
| --- | --- | --- | --- | --- |
| employeeId | + | number / (формат: integer($int64)) | history.employees.employee_id | Идентификатор сотрудника |
| id | + | number / (формат: integer($int64)) | history.employees.id | Идентификатор записи |
| changedField | + | string | history.employees.changed_field | Измененное поле |
| fieldDataType | + | string / (формат: enum) | history.employees.field_data_type | Тип измененного поля |
| previousValue | - | string | history.employees.previous_value | Предыдущее значение |
| newValue | - | string | history.employees.new_value | Новое значение |
| updatedBy | + | string / (формат: date-time) | history.employees.updated_by | Кто изменил |
| updatedAt | + | string / (формат: date-time) | history.employees.updated_at | Когда было изменено |

| [ / { / "id": 1, / "employeeId": 10, / "changedField": "Фамилия", / "fieldDataType": "STRING", / "previousValue": "Иванов", / "newValue": "Петров", / "updatedBy": "Пупкин Петр", / "updatedAt": "2025-03-15T13:11:10.74573" / }, / { / "id": 2, / "employeeId": 10, / "changedField": "Тип сотрудника", / "fieldDataType": "STRING", / "previousValue": "Внутренний", / "newValue": "Внешний", / "updatedBy": "Иванов Иван", / "updatedAt": "2025-03-20T13:11:10.74573" / }, / { / "id": 3, / "employeeId": 10, / "changedField": "Руководитель", / "fieldDataType": "STRING", / "previousValue": "Лебедев Илья", / "newValue":  **null**, / "updatedBy": "Иванов Иван", / "updatedAt":  "2025-03-20T13:11:10.74573" / }, / { / "id": 4, / "employeeId": 10, / "changedField": "Внешний менеджер", / "fieldDataType": "STRING", / "previousValue": **null**, / "newValue":  "Карась Николай", / "updatedBy": "Иванов Иван", / "updatedAt":  "2025-03-20T13:11:10.74573" / } / ] / } |
| --- |
