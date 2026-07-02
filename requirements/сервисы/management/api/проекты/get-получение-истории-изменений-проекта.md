# Получение истории изменений проекта

**GET** `/management/projects/{projectId}/history`

Получение истории изменений проекта
**Описание метода:**
Метод предназначен для получения истории изменений конкретного проекта.
Метод: GET
Эндпоинт: /management/projects/{projectId}/history
**Строка запроса: **GET /management/projects/{projectId}/history
**Пример запроса:**  GET /management/projects/10/history
**Пример ответа:**
200 OK

| Название параметра | Обязательность | Тип данных | Мэппинг на БД | Описание |
| --- | --- | --- | --- | --- |
| projectId | + | number / (формат: integer($int64)) | history.projects.project_id | Идентификатор проекта |
| id | + | number / (формат: integer($int64)) | history.projects.id | Идентификатор записи |
| changedField | + | string | history.projects.changed_field | Измененное поле |
| fieldDataType | + | string / (формат: enum) | history.projects.field_data_type | Тип измененного поля |
| previousValue | - | string | history.projects.previous_value | Предыдущее значение |
| newValue | - | string | history.projects.new_value | Новое значение |
| updatedBy | + | string / (формат: date-time) | history.projects.updated_by | Кто изменил |
| updatedAt | + | string / (формат: date-time) | history.projects.updated_at | Когда было изменено |

| [ / { / "id": 1, / "projectId": 10, / "changedField": "Менеджер", / "fieldDataType": "STRING", / "previousValue": "Иванов Иван", / "newValue": "Петров Филипп", / "updatedBy": "Пупкин Петр", / "updatedAt": "2025-03-10T13:11:10.74573" / }, / { / "id": 2, / "projectId": 10, / "changedField": "Код проекта", / "fieldDataType": "ARRAY_STRING", / "previousValue": "чк1; чк2; чк3", / "newValue": "чк1; чк3; чк4; чк5", / "updatedBy": "Иванов Иван", / "updatedAt": "2025-03-20T13:11:10.74573" / } / ] |
| --- |
