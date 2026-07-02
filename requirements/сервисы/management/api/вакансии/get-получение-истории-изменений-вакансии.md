# Получение истории изменений вакансии

**GET** `/management/vacancies/{vacancyId}/history`

Получение истории изменений вакансии
**Описание метода:**
Метод предназначен для получения истории изменений конкретной вакансии.
Метод: GET
Эндпоинт: /management/vacancies/{vacancyId}/history
**Строка запроса: **GET /management/vacancies/{vacancyId}/history
**Пример запроса:**  GET /management/vacancies/10/history
**Пример ответа:**
200 OK

| Название параметра | Обязательность | Тип данных | Мэппинг на БД | Описание |
| --- | --- | --- | --- | --- |
| vacancyId | + | number / (формат: integer($int64)) | history.vacancies.vacancy_id | Идентификатор вакансии |
| id | + | number / (формат: integer($int64)) | history.vacancies.id | Идентификатор записи |
| changedField | + | string | history.vacancies.changed_field | Измененное поле |
| fieldDataType | + | string / (формат: enum) | history.vacancies.field_data_type | Тип измененного поля |
| previousValue | - | string | history.vacancies.previous_value | Предыдущее значение |
| newValue | - | string | history.vacancies.new_value | Новое значение |
| updatedBy | + | string / (формат: date-time) | history.vacancies.updated_by | Кто изменил |
| updatedAt | + | string / (формат: date-time) | history.vacancies.updated_at | Когда было изменено |

| [ / { / "id": 1, / "vacancyId": 10, / "changedField": "Метка", / "fieldDataType": "ARRAY_STRING", / "previousValue": "ЦФТ", / "newValue": "ЦФТ; Кафка", / "updatedBy": "Пупкин Петр", / "updatedAt": "2025-03-15T13:11:10.74573" / }, / { / "id": 2, / "vacancyId": 10, / "changedField": "Кто обрабатывает", / "fieldDataType": "ARRAY_STRING", / "previousValue": "Иванов Николай; Петров Петр", / "newValue": "Иванов Николай; Пупкина Наталья; Лебедев Кирилл", / "updatedBy": "Иванов Иван", / "updatedAt": "2025-03-20T13:11:10.74573" / } / ] |
| --- |
