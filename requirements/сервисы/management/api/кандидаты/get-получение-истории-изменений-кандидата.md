# Получение истории изменений кандидата

**GET** `/management/candidates/{candidateId}/history`

Получение истории изменений кандидата
**Описание метода:**
Метод предназначен для получения истории изменений конкретного кандидата.
Метод: GET
Эндпоинт: /management/candidates/{candidateId}/history
**Строка запроса: **GET /management/candidates/{candidateId}/history
**Пример запроса:**  GET /management/candidates/{10}/history
**Пример ответа:**
200 OK

| Название параметра | Обязательность | Тип данных | Мэппинг на БД | Описание |
| --- | --- | --- | --- | --- |
| candidateId | + | number / (формат: integer($int64)) | history.candidates.candidate_id | Идентификатор кандидата |
| id | + | number / (формат: integer($int64)) | history.candidates.id | Идентификатор записи |
| changedField | + | string | history.candidates.changed_field | Измененное поле |
| fieldDataType | + | string / (формат: enum) | history.candidates.field_data_type | Тип измененного поля |
| previousValue | - | string | history.candidates.previous_value | Предыдущее значение |
| newValue | - | string | history.candidates.new_value | Новое значение |
| updatedBy | + | string / (формат: date-time) | history.candidates.updated_by | Кто изменил |
| updatedAt | + | string / (формат: date-time) | history.candidates.updated_at | Когда было изменено |

| [ / { / "id": 1, / "candidateId": 10, / "changedField": "ФИО", / "fieldDataType": "STRING", / "previousValue": "Иванов И.", / "newValue": "Иванов Иван", / "updatedBy": "Пупкин Петр", / "updatedAt": "2025-03-10T13:11:10.74573" / }, / { / "id": 2, / "candidateId": 10, / "changedField": "Дата интервью (внутр.)", / "fieldDataType": "ARRAY_DATE", / "previousValue": "10.01.2025", / "newValue": "10.01.2025; 10.02.2025", / "updatedBy": "Иванов Иван", / "updatedAt": "2025-03-20T13:11:10.74573" / } / ] |
| --- |

##### Swagger

#### API назначений

##### История изменений

| Дата | Автор | Описание |
| --- | --- | --- |
| 10.03.2025 |  | Изменено описание массива paymentDates при создании и редактировании назначений |
| 25.03.2025 |  | Добавлено описание валидации циклической зависимости в методе изменения сотрудника |
| 18.07.2025 |  | Дополнены описания методов для работы с сотрудниками: добавлены параметры fileUuid, file |

##### Описание API

###### Методы для работы с ролями и грейдами
