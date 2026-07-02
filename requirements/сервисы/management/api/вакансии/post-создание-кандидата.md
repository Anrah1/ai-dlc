# Создание кандидата

**POST** `/management/vacancies/{id}/candidates`

Описание
**Описание метода:**
Метод предназначен для создания нового кандидата
Валидации:
Метод: POST
Эндпоинт: https://management/vacancies/{id}/candidates
**Строка** **запроса****:** POST https://management/vacancies/{id}/candidates

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| id | number / (формат: integer($int64)) | + | Идентификатор вакансии, по которой процессится кандидат<br>path-параметр | planer.vacancies.id |
| **Тело запроса** | **Тело запроса** | **Тело запроса** | **Тело запроса** | **Тело запроса** |
| fullName | string | + | ФИО кандидата | planer.candidates.full_name |
| wherefrom | string | + | Где нашли кандидата (источник поиска) | planer.candidates.wherefrom |
| interviewers | array | - | Интервьюеры |  |
| id | number / (формат: integer($int64)) | - | Идентификатор интервьюера (сотрудника проводившего интервью) | planer.employees.id |
| screeningFeedback | string | - | ОС по скринингу (внутреннему интервью) | planer.candidates.screening_feedback |
| customerFeedback | string | - | ОС от заказчика | planer.candidates.customer_feedback |
| interviews | array[object] | - | Интервью |  |
| id | number / (формат: integer($int64)) | - | Идентификатор даты | planer.interviews.id / (передается в запросе null) |
| date | string / (формат:$date)) | - | Дата в формате YYYY-MM-DD | planer.interviews.date |
| type | string / (формат: enum) | - | Тип интервью (Внутреннее/Внешнее) | planer.interviews.type |
| fileUuid | uuid | - | UUID- Универсальный уникальный идентификатор (uuid) файла  резюме в хранилище | planer.candidates.file_uuid |
| comment | string | - | Комментарий | planer.candidates.comment |
| status | string / (формат: enum) | + | Статус кандидата | planer.candidates.status |
| audioUuid | uuid | - | UUID- Универсальный уникальный идентификатор (uuid) аудио записи в хранилище | planer.candidates.audio_uuid |

| При создании кандидата (в запросе) не отправлять поле file или name / На беке убрать это поле из requestDto — не придется в маппере игнорить. Для обновления этого поля использовать отдельный метод ниже |
| --- |

**Пример запроса:**

| { / "fullName": "Смирнов Дмитрий", / "wherefrom": "от Лиги", / "interviewers": [ / 21, / 12 / ], / "screeningFeedback": "Классно, круто, умный парень, шарит за кафку, 10 из 10", / "customerFeedback": "Хороший, классные софт скиллы, знает, о чем говорит", / "interviews": [ / { / "id": **null**, / "date": "2025-02-05", / "type": "INTERNAL" / }, / { / "id": **null**, / "date": "2025-02-15", / "type": "INTERNAL" / }, / { / "id": **null**, / "date": "2025-03-05", / "type": "EXTERNAL" / }, / { / "id": **null**, / "date": "2025-03-07", / "type": "EXTERNAL" / } / ], / "fileUuid": "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11", / "comment": **null**, / "status": "PLANNED_INTERNAL_INTERVIEW" / } |
| --- |

**Ответ:**

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| id | number / (формат: integer($int64)) | + | Идентификатор кандидата | planer.candidates.id |
| vacancyId | number / (формат: integer($int64)) | + | Идентификатор вакансии | planer.candidates.vacancy_id |
| fullName | string | + | ФИО кандидата | planer.candidates.full_name |
| wherefrom | string | + | Где нашли кандидата (источник поиска) | planer.candidates.wherefrom |
| interviewers | array[object] | - | Интервьюеры |  |
| id | number / (формат: integer($int64)) | - | Идентификатор интервьюера (сотрудника проводившего интервью) | planer.employees.id |
| lastName | string | - | Фамилия сотрудника | planer.employees.last_name |
| firstName | string | - | Имя сотрудника | planer.employees.first_name |
| screeningFeedback | string | - | ОС по скринингу (внутреннему интервью) | planer.candidates.screening_feedback |
| customerFeedback | string | - | ОС от заказчика | planer.candidates.customer_feedback |
| interviews | array[object] | - | Интервью |  |
| id | number / (формат: integer($int64)) | - | Идентификатор даты | planer.interviews.id |
| date | string / (формат:$date) | - | Дата в формате YYYY-MM-DD | planer.interviews.date |
| type | string / (формат: enum) | - | Тип интервью (Внутреннее/Внешнее) | planer.interviews.type |
| file | object | - |  |  |
| id | uuid | - | Универсальный уникальный идентификатор (uuid) файла  резюме в хранилище |  |
| name | string | - | Название файла резюме |  |
| link | string | - | Ссылка на скачивание из хранилища / *Время жизни 1 час или до первого скачивания |  |
| comment | string | - | Комментарий | planer.candidates.comment |
| status | string / (формат: enum) | + | Статус кандидата | planer.candidates.status |
| audio | object | - |  |  |
| id | uuid | - | Универсальный уникальный идентификатор (uuid) аудио записи в хранилище |  |
| name | string | - | Название аудио записи |  |
| link | string | - | Ссылка на скачивание из хранилища / *Время жизни 1 час или до первого скачивания |  |

**Пример успешного ответа**
201 Created: Кандидат успешно создан

| { / "id": 24, / "vacancyId": 10, / "fullName": "Смирнов Дмитрий", / "wherefrom": "от Лиги", / "interviewers": [ / { / "id": 21, / "lastName": "Кузина", / "firstName": "Наталья" / }, / { / "id": 12, / "lastName": "Воронин", / "firstName": "Константин" / } / ], / "screeningFeedback": "Классно, круто, умный парень, шарит за кафку, 10 из 10", / "customerFeedback": "Хороший, классные софт скиллы, знает, о чем говорит", / "interviews": [ / { / "id": 1, / "date": "2025-02-05", / "type": "INTERNAL" / }, / { / "id": 2, / "date": "2025-02-15", / "type": "INTERNAL" / }, / { / "id": 3, / "date": "2025-03-05", / "type": "EXTERNAL" / }, / { / "id": 4, / "date": "2025-03-07", / "type": "EXTERNAL" / } / ], / "file": { / "id": "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11", / "name": "CV_Смирнов Д.", / "link" : "dfFzfdxdfxdgfxfg" / }, / "comment": **null**, / "status": "PLANNED_INTERNAL_INTERVIEW" / } |
| --- |

**Ошибки:**
400 Bad Request: Некорректные данные запроса

| {"message": "Поле <название атрибута> не может быть пустым.; Поле <название атрибута 2> не может быть пустым."} / Разделитель между ошибками ; / Валидно для обязательных атрибутов: ФИО, Откуда, Статус. |
| --- |

404 Not Found: Сотрудник/вакансия не найден.

| { / "message": "Сотрудник с идентификатором 'employeeId' не найден." / } / { / "message": "Вакансия с идентификатором 'vacancyId' не найдена." / } |
| --- |
