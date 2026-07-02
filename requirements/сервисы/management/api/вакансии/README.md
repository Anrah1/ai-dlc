# API: вакансии

Методы группы «вакансии».

| Метод | Эндпоинт | Описание |
| --- | --- | --- |
| GET | `/management/vacancies` | [Получение списка всех вакансий](get-получение-списка-всех-вакансий.md) |
| POST | `/management/vacancies` | [Создание вакансии](post-создание-вакансии.md) |
| POST | `/management/vacancies/ai/{vacancyId}` | [Создание кандидата при помощи ИИ](post-создание-кандидата-при-помощи-ии.md) |
| GET | `/management/vacancies/{id}` | [Получение информации о конкретной вакансии](get-получение-информации-о-конкретной-вакансии.md) |
| PUT | `/management/vacancies/{id}` | [Редактирование вакансии](put-редактирование-вакансии.md) |
| POST | `/management/vacancies/{id}/candidates` | [Создание кандидата](post-создание-кандидата.md) |
| PUT | `/management/vacancies/{vacancyId}/candidates/{candidateId}` | [Редактирование кандидата](put-редактирование-кандидата.md) |
| GET | `/management/vacancies/{vacancyId}/history` | [Получение истории изменений вакансии](get-получение-истории-изменений-вакансии.md) |

