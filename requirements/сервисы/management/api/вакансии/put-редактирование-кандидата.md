# Редактирование кандидата

**PUT** `/management/vacancies/{vacancyId}/candidates/{candidateId}`

Описание
**Описание метода:**
Метод предназначен для редактирования кандидата.
**Логика выполнения метода:**
После получения данных выполняется валидация:
Проверка заполнения обязательных полей: vacancyId, candidateId, fullName, wherefrom, status.
Проверка существования id для сотрудника, кандидата, вакансии, иначе вызывается ошибка 404.
После успешной валидации выполняется сбор информации об изменении (аудит). Происходит сравнение старой записи с новыми полученными данными. В аудит входит:
Идентификатор изменяемой записи (candidate_id);
Название изменяемых полей (changed_field);
Тип изменяемых полей (field_data_type);
Старые и новые значения данных (previous_value и new_value);
Временная метка изменения (updated_at);
ФИ пользователя, внесшего изменения (updated_by).
Далее аудит отправляется в БД: схему history, таблицу candidates, подробнее в описании .
3. Новые значения записи (полученные данные) обновляются в БД: схеме planer, таблице candidates.
Метод:  PUT
Эндпоинт: https://management/vacancies/{vacancyId}/candidates/{candidateId}
**Строка** **запроса****:** PUT https://management/vacancies/{vacancyId}/candidates/{candidateId}

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| vacancyId | number / (формат: integer($int64)) | + | Идентификатор вакансии, по которой процессится кандидат<br>path-параметр | planer.vacancies.id |
| candidateId | number / (формат: integer($int64)) | + | Идентификатор кандидата / path-параметр | planer.candidates.id |
| **Тело запроса** | **Тело запроса** | **Тело запроса** | **Тело запроса** | **Тело запроса** |
| fullName | string | + | ФИО кандидата | planer.candidates.full_name |
| wherefrom | string | + | Где нашли кандидата (источник поиска) | planer.candidates.wherefrom |
| interviewers | array | - | Интервьюеры |  |
| id | number / (формат: integer($int64)) | - | Идентификатор интервьюера (сотрудника проводившего интервью) | planer.candidates_interviewers.interviewer_id |
| screeningFeedback | string | - | ОС по скринингу (внутреннему интервью) | planer.candidates.screening_feedback |
| customerFeedback | string | - | ОС от заказчика | planer.candidates.customer_feedback |
| interviews | array[object] | - | Интервью |  |
| id | number / (формат: integer($int64)) | - | Идентификатор даты | planer.interviews.id |
| date | string / (формат:$date) | - | Дата в формате YYYY-MM-DD | planer.interviews.date |
| type | string / (формат: enum) | - | Тип интервью (Внутреннее/Внешнее) | planer.interviews.type |
| fileUuid | uuid | - | UUID- Универсальный уникальный идентификатор (uuid) файла  резюме в хранилище | planer.candidates.file_uuid |
| comment | string | - | Комментарий | planer.candidates.comment |
| status | string / (формат: enum) | + | Статус | planer.candidates.status |
| audioUuid | uuid | - | UUID- Универсальный уникальный идентификатор (uuid) аудио записи в хранилище | planer.candidates.audio_uuid |

**Пример запроса:** PUT management/vacancies/10/candidates/24

| { / "fullName": "Смирнов Дмитрий", / "wherefrom": "от Лиги", / "interviewers": [ / 12  //удалили интервьюера с id=21 / ], / "screeningFeedback": "Классно, круто, умный парень, шарит за кафку, 10 из 10", / "customerFeedback": "Хороший, классные софт скиллы, знает, о чем говорит", / "interviews": [ / { / "id": 1, / "date": "2025-02-07", / "type": "INTERNAL" / }, / { / "id": 2, / "date": "2025-02-15", / "type": "INTERNAL" / }, / { / "id": 4, / "date": "2025-03-07", / "type": "EXTERNAL" / } / ], / "fileUuid": "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11", / "comment": **null**, / "status": "PLANNED_INTERNAL_INTERVIEW" / } |
| --- |

**Работа с датами:**
Описание
При обновлении поля interviews у кандидата мы передаем полный список объектов, который хотим получить в результате.
Пусть у нас поле interviews имеет следующий исходный вид:

| "interviews": [ / { / "id": 1, / "date": "2025-02-05" / }, / { / "id": 2, / "date": "2025-02-15" / } / ] |
| --- |

**Кейс1**: обновили первую дату в массиве interviews с id = 1, тогда запрос на редактирование кандидата будет выглядеть следующим образом:

| "interviews": [ / { / "id": 1, / "date": "2025-02-07"  //Поменяли дату с 2025-02-05 на 2025-02-07 / }, / { / "id": 2, / "date": "2025-02-15" / } / ] |
| --- |

| При этом второй объект datesOfInterview мы не изменяли, но должны также передать его, иначе он удалится! |
| --- |

**Кейс2:** обновление кандидата с удалением записи interviews. например мы удалили записи с  id=2, из предыдущего примера (кейс1)
Поле в запросе в таком случае будет выглядеть следующим образом:

| "interviews": [ / { / "id": 1, / "date": "2025-02-07" / } / ] |
| --- |

**Кейс3:** обновление кандидата и добавление новой записи  interviews,
Поле в запросе будет выглядеть следующим образом:

| "interviews": [ / { / "id": 1, / "date": "2025-02-07" / }, / { / "id": **null**, / "date": "2025-02-17" / } / ] |
| --- |

**Кейс4:** обновляем кандидата и удаляем все interviews. Поле в запросе будет выглядеть следующим образом

| "interviews": [ / //пустой массив / ] |
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
| link | string | - | Ссылка на скачивание из хранилища |  |
| comment | string | - | Комментарий | planer.candidates.comment |
| status | string / (формат: enum) | + | Статус | planer.candidates.status |
| audio | object | - |  |  |
| id | uuid | - | Универсальный уникальный идентификатор (uuid) аудио записи в хранилище |  |
| name | string | - | Название аудио записи |  |
| link | string | - | Ссылка на скачивание из хранилища / *Время жизни 1 час или до первого скачивания |  |

**Пример успешного ответа:**
200 ОК: Данные кандидата успешно обновлены.

| { / "id": 24, / "vacancyId": 10, / "fullName": "Смирнов Дмитрий", / "wherefrom": "от Лиги", / "interviewers": [ / { / "id": 12, / "lastName": "Воронин", / "firstName": "Константин" / } / ], / "screeningFeedback": "Классно, круто, умный парень, шарит за кафку, 10 из 10", / "customerFeedback": "Хороший, классные софт скиллы, знает, о чем говорит", / "interviews": [ / { / "id": 1, / "date": "2025-02-07", / "type": "INTERNAL" / }, / { / "id": 2, / "date": "2025-02-15", / "type": "INTERNAL" / }, / { / "id": 4, / "date": "2025-03-07", / "type": "EXTERNAL" / } / ], / "file": { / "id": "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11", / "name": "CV_Смирнов Д.", / "link" : "dfFzfdxdfxdgfxfg" / }, / "comment": **null**, / "status": "PLANNED_INTERNAL_INTERVIEW" / } |
| --- |

**Ошибки:**
400 Bad Request: Некорректные данные запроса

| { / "message": "Поле <название атрибута> не может быть пустым.; Поле <название атрибута 2> не может быть пустым." / } / Разделитель между ошибками ; / Валидно для обязательных атрибутов: ФИО, Откуда, Статус. |
| --- |

404 Not Found: Сотрудник/дата/кандидат/вакансия не найден.

| { / "message": "Сотрудник с идентификатором 'employeeId' не найден." / } / { / "message": "Кандидат с идентификатором 'candidateId' не найден." / } / { / "message": "Вакансия с идентификатором 'vacancyId' не найдена." / } |
| --- |
