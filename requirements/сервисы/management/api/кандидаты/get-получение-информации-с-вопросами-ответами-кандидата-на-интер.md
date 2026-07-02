# Получение информации с вопросами-ответами кандидата на интервью

**GET** `/management/candidates/{candidateId}/interview-results`

Описание
**Описание метода:**
Метод предназначен для получения информации с интервью кандидата (вопросы-ответы).
Метод: GET
Эндпоинт: https://management/candidates/{candidateId}/interview-results
**Строка** **запроса****:** GET https://management/candidates/{candidateId}/interview-results
**Пример запроса:** GET https://management/candidates/10/interview-results
**Ответ:**
Массив из объектов:

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| id | number / (формат: integer ($int64)) | + | Идентификатор записи | planer.interview_results.id |
| candidateId | number / (формат: integer ($int64)) | + | Идентификатор кандидата | planer.interview_results.candidate_id |
| questionText | string | + | Текст вопроса | planer.interview_results.question_text |
| answerText | string | - | Текст ответа | planer.interview_results.answer_text |

**Пример успешного ответа:**
200 ОК: Данные отправлены.

| [ / { / "id": 1, / "candidateId": 10, / "questionText": "Что такое UC?", / "answerText": "Cценарное описание взаимодействия пользователя с программным продуктом для достижения конкретной цели." / }, / { / "id": 2, / "candidateId": 10, / "questionText": "Функции Use Case", / "answerText": "Документация требований, описание поведения системы, идентификация участников, планирование тестирования." / } / ] |
| --- |

**Ошибки:**
404 Not Found: Кандидат не найден.

| { / "message": "Кандидат с идентификатором 'id' не найден." / } |
| --- |
