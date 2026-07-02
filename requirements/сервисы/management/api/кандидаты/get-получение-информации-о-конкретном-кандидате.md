# Получение информации о конкретном кандидате

**GET** `/management/candidates/{candidateId}`

Описание
**Описание метода:**
Метод предназначен для получения информации о конкретном кандидате.
Метод:  GET
Эндпоинт: https://management/candidates/{candidateId}
**Строка** **запроса****:** GET https://management/candidates/{candidateId}
**Пример запроса:** GET https://management/candidates/5
**Ответ:**

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| id | number / (формат: integer($int64)) | + | Идентификатор кандидата | planer.candidates.id |
| vacancyId | number / (формат: integer($int64)) | + | Идентификатор вакансии | planer.candidates.vacancy_id |
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
| file | object | - |  |  |
| id | uuid | - | Универсальный уникальный идентификатор (uuid) файла  резюме в хранилище |  |
| name | string | - | Название файла резюме |  |
| link | string | - | Ссылка на скачивание из хранилища |  |
| comment | string | - | Комментарий | planer.candidates.comment |
| aiMatch | object | - | Объект с последним результатом ИИ‑матчинга |  |
| scorePercent | decimal | - | Процент соответствия | planer.candidate_ai_match.score_percent |
| summaryText | string | - | Текст совпадения навыков | planer.candidate_ai_match.summary_text |
| model | string | - | Модель ИИ | planer.candidate_ai_match.model |
| promptVersion | string | - | Версия промпта | planer.candidate_ai_match.prompt_version |
| createdAt | timestamp | - | Дата и время создания | planer.candidate_ai_match.created_at |
| inputResumeFileUuid | uuid | - | UUID резюме | planer.candidate_ai_match.input_resume_file_uuid |
| jobId | uuid | - | ID джоба по создания резюме по ИИ | planer.candidate_ai_match.job_id |
| status | string | + | Статус | planer.candidates.status |
| audio | object | - |  |  |
| id | uuid | - | Универсальный уникальный идентификатор (uuid) аудио записи в хранилище |  |
| name | string | - | Название аудио записи |  |
| link | string | - | Ссылка на скачивание из хранилища / *Время жизни 1 час или до первого скачивания |  |

**Пример успешного ответа:**
200 ОК: Данные по кандидатам вакансии отправлены.

| { / "id": 7, / "vacancyId": 7, / "fullName": "Смирнов Дмитрий", / "wherefrom": "от Лиги", / "interviewers": [ / { / "id": 21, / "lastName": "Кузина", / "firstName": "Наталья" / }, / { / "id": 12, / "lastName": "Воронин", / "firstName": "Константин" / } / ], / "screeningFeedback": "Классно, круто, умный парень, шарит за кафку, 10 из 10", / "customerFeedback": "Хороший, классные софт скиллы, знает, о чем говорит", / "interviews": [ / { / "id": 1, / "type": "INTERNAL", / "date": "2024-02-05" / }, / { / "id": 2, / "type": "EXTERNAL", / "date": "2024-02-15" / } / ], / "file": { / "id": "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11", / "name": "CV_Смирнов Д._2025-02-03T18:11:10.74573", / "link" : "dfFzfdxdfxdgfxfg" / }, / "comment": **null**, / "aiMatch": { / "vacancyId": "3fa85f64-5717-4562-b3fc-2c963f66afa6", / "scorePercent": 85.5, / "summaryText": "Навыки кандидата соответствуют требованиям вакансии на 85.5%...", / "model": "gpt-4", / "promptVersion": "v2.1", / "createdAt": "2025-02-24T10:35:00Z", / "inputResumeFileUuid": "3fa85f64-5717-4562-b3fc-2c963f66afa6", / "jobId": "9f1a8c32-e5b7-4d3f-9a2c-1e8b6f7d4a3b" / }, / "jobId": "a0eebc99-9c0b-4ef8-bb6d-6bb7bd380a34", / "status": "PLANNED_INTERNAL_INTERVIEW" / } |
| --- |

**Ошибки:**
404 Not Found: Кандидат не найден.

| { / "message": "Кандидат с идентификатором 'id' не найден." / } |
| --- |
