# Получение списка кандидатов

**GET** `/management/candidates`

Описание
**Описание метода:**
Метод предназначен для получения списка всех кандидатов.
Метод:  GET
Эндпоинт: https://management/candidates
**Строка** **запроса****:** GET https://management/candidates?vacancyId={vacancyId}
**Параметры**:
Если необходимо получить список кандидатов вакансии, то используется query-параметр:

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| vacancyId | number / (формат: integer($int64)) | + | Идентификатор вакансии, по которой выводится список кандидатов<br>query-параметр | planer.candidates.vacancy_id |

**Пример запроса:** GET https://management/candidates?vacancyId=7
**Ответ:**
Массив из объектов:

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| id | number / (формат: integer($int64)) | + | Идентификатор кандидата | planer.candidates.id |
| vacancy | object | + | Вакансия |  |
| id | number / (формат: integer($int64)) | + | Идентификатор вакансии | planer.vacancies.id |
| role | object | + | Роль |  |
| id | number / (формат: integer($int32)) | + | Идентификатор роли | planer.roles.id |
| name | string | + | Название роли | planer.roles.name |
| subrole | object | - | Подроль |  |
| id | number / (формат: integer($int32)) | - | Идентификатор подроли | planer.subroles.id |
| name | string | - | Название подроли | planer.suboles.name |
| grade | string | + | Грейд(ы), разделитель ";" | planer.vacancies.grades |
| project | object | + | Проект |  |
| id | number / (формат: integer($int64)) | + | Идентификатор проекта | planer.projects.id |
| name | string | + | Название проекта | planer.projects.name |
| tribe | string | - | Трайб/команда | planer.vacancies.tribe |
| quantityOfEmployees | number / (формат: integer($int32)) | + | Количество требуемых сотрудников | planer.vacancies.quantity_of_employees |
| periodOfAttraction | string | - | Срок привлечения | planer.vacancies.period_of_attraction |
| customers | string | - | Заказчики | planer.vacancies.customers |
| tags | string | - | Теги/метки, разделитель ";" | planer.vacancies.tags |
| requirements | string | - | Требования | planer.vacancies.requirements |
| comment | string | - | Комментарий | planer.vacancies.comment |
| dateOfRequest | string / (формат: date) | + | Дата обращения | planer.vacancies.date_of_request |
| status | string | + | Статус | planer.vacancies.status |
| location | string | + | Локация | planer.vacancies.location |
| vendorRate | string | - | Ставка для Вендора | planer.vacancies.vendor_rate |
| experience | string | - | Опыт (лет) | planer.vacancies.experience |
| urgency | string <br>(формат: enum) | - | Срочность | planer.vacancies.urgency |
| fullName | string | + | ФИО кандидата | planer.candidates.full_name |
| wherefrom | string | + | Где нашли кандидата | planer.candidates.wherefrom |
| interviewers | array[object] | - | Интервьюеры |  |
| id | number / (формат: integer($int64)) | - | Идентификатор интервьюера (сотрудника проводившего интервью) | planer.employees.id |
| lastName | string | - | Фамилия сотрудника | planer.employees.last_name |
| firstName | string | - | Имя сотрудника | planer.employees.first_name |
| screeningFeedback | string | - | ОС по скринингу (внутреннему интервью) | planer.candidates.screening_feedback |
| customerFeedback | string |  | ОС от заказчика | planer.candidates.customer_feedback |
| interviews | array[object] | - | Даты внутреннего собеседования |  |
| id | number / (формат: integer($int64)) | - | Идентификатор даты | planer.interviews.id |
| type | string | - | Тип интервью | planer.interviews.type |
| date | string / (формат: date) | - | Дата | planer.interviews.date |
| comment | string | - | Комментарий | planer.candidates.comment |
| status | string | + | Статус | planer.candidates.status |
| createdAt | string / (формат: date-time) | + | Дата создания | planer.candidates.createdAt |
| updatedAt | string / (формат: date-time) | + | Дата обновления | planer.candidates.updatedAt |

**Пример успешного ответа:**
200 ОК: Данные кандидатов отправлены.

| [ / { / "id": 7, / "vacancy": { / "id": 7, / "role": { / "id": 3, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Бизнес" / }, / "grade": "Senior", / "project": { / "id": 10, / "name": "Проект А" / }, / "tribe": "Планшеты", / "quantityOfEmployees": 3, / "periodOfAttraction": "На квартал", / "customers": "Смирнов, smir@sm.ru", / "tags": "ЦФТ, Camunda", / "requirements": "Микросервисы, Siebel, React, Rabbit, Kafka", / "comment": "Желательно из финтеха", / "dateOfRequest": "2025-02-10", / "status": "IN_PROGRESS", / "location": "СНГ", / "vendorRate": "50 000", / "experience": "3+", / "urgency": "Срочно" / }, / "fullName": "Смирнов Дмитрий", / "wherefrom": "от Лиги", / "interviewers": [ / { / "id": 21, / "lastName": "Кузина", / "firstName": "Наталья" / }, / { / "id": 12, / "lastName": "Воронин", / "firstName": "Константин" / } / ], / "screeningFeedback": "Классно, круто, умный парень, шарит за кафку, 10 из 10", / "customerFeedback": "Хороший, классные софт скиллы, знает, о чем говорит", / "interviews": [ / { / "id": 1, / "type": "INTERNAL", / "date": "2024-02-05" / }, / { / "id": 2, / "type": "EXTERNAL", / "date": "2024-02-15" / } / ], / "comment": **null**, / "status": "PLANNED_INTERNAL_INTERVIEW", / "createdAt": "2024-12-20T14:14:10.74573", / "updatedAt": "2025-02-03T18:11:10.74573" / }, / { / "id": 8, / "vacancy": { / "id": 9, / "role": { / "id": 3, / "name": "Аналитик" / }, / "subrole": { / "id": 1, / "name": "Бизнес" / }, / "grade": "Senior", / "project": { / "id": 10, / "name": "Проект А" / }, / "tribe": "Планш", / "quantityOfEmployees": 3, / "periodOfAttraction": "На квартал", / "customers": "Смирнов, smir@sm.ru", / "tags": "ЦФТ, Camunda", / "requirements": "Микросервисы, Siebel, React, Rabbit, Kafka", / "comment": "Желательно из финтеха", / "dateOfRequest": "2025-02-10", / "status": "IN_PROGRESS", / "location": "СНГ", / "vendorRate": "50 000", / "experience": "3+", / "urgency": "Срочно" / }, / "fullName": "Иванова Мария", / "wherefrom": "от Лиги", / "interviewers": [ / { / "id": 21, / "lastName": "Кузина", / "firstName": "Наталья" / }, / { / "id": 12, / "lastName": "Воронин", / "firstName": "Константин" / } / ], / "screeningFeedback": "Молодец, знает многое", / "customerFeedback": "Понравилась, захотели взять", / "interviews": [ / { / "id": 3, / "typeOfInterview": "INTERNAL", / "date": "2024-02-05" / }, / { / "id": 4, / "typeOfInterview": "EXTERNAL", / "date": "2024-02-15" / } / ], / "comment": "коммент", / "status": "PLANNED_INTERNAL_INTERVIEW", / "createdAt": "2024-12-20T14:14:10.74573", / "updatedAt": "2025-02-03T18:11:10.74573" / } / ] |
| --- |

**Ошибки:**
204 No Content: Запрос выполнен успешно, но в ответе отсутствует контент.

| { / } |
| --- |

Описание
**Описание метода:**
Метод предназначен для получения статуса ИИ обработки резюме.
Метод:  GET
Эндпоинт: https://management/candidates/ai/{jobId}
**Строка** **запроса****:** GET https://management/candidates/ai/{jobId}
**Пример запроса:** GET https://management/candidates/ai/5
**Ответ:**

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| jobId | uuid | + | Идентификатор работы джоба | planer.candidate_ai_match.job_id |
| status | string | + | Статус обработки | planer.candidate_ai_match.status |
| candidateId | uuid | + | Идентификатор кандидата | planer.candidate_ai_match.candidate_id |
| vacancyId | uuid | + | Идентификатор вакансии | planer.candidate_ai_match.vacancy_id |
| result | object | - | Объект с результатом обработки (присутствует, если status = COMPLETED) |  |
| scorePercent | decimal | - | Процент соответствия | planer.candidate_ai_match.score_percent |
| summaryText | string | - | Текст сравнения навыков | planer.candidate_ai_match.summary_text |
| model | string | - | Модели ИИ | planer.candidate_ai_match.model |
| promptVersion | string | - | Версия промпта | planer.candidate_ai_match.promt_version |
| createdAt | timestamp | - | Дата и время создания | planer.candidate_ai_match.created_at |
| errorMessage | string | - | Сообщение об ошибке (присутствует, если status = FAILED) |  |

**Пример успешного ответа:**
200 ОК: Данные по ии обработке резюме отправлены.

| { / "jobId": "9f1a8c32-e5b7-4d3f-9a2c-1e8b6f7d4a3b", / "status": "COMPLETED", / "candidateId": "3fa85f64-5717-4562-b3fc-2c963f66afa6", / "vacancyId": "3fa85f64-5717-4562-b3fc-2c963f66afa6", / "result": { / "scorePercent": 85.5, / "summaryText": "Навыки кандидата соответствуют требованиям вакансии на 85.5%", / "model": "gpt-4", / "promptVersion": "v2.1", / "createdAt": "2025-02-24T10:35:00Z" / }, / "errorMessage": "string" / } |
| --- |

**Ошибки:**
404 Not Found: JobId не найден.

| { / "message": "JobId с идентификатором 'id' не найден." / } |
| --- |
