# API сервиса management

Базовый префикс: `/management`

## По группам

| Группа | Индекс | Методов |
| --- | --- | --- |
| вакансии | [вакансии](вакансии/README.md) | 8 |
| кандидаты | [кандидаты](кандидаты/README.md) | 6 |
| назначения | [назначения](назначения/README.md) | 7 |
| проекты | [проекты](проекты/README.md) | 5 |
| роли | [роли](роли/README.md) | 1 |
| сотрудники | [сотрудники](сотрудники/README.md) | 6 |
| файлы | [файлы](файлы/README.md) | 1 |

## Полный список

| Метод | Эндпоинт | Описание | Группа |
| --- | --- | --- | --- |
| GET | `/management/vacancies` | Получение списка всех вакансий | [вакансии](вакансии/README.md) |
| POST | `/management/vacancies` | Создание вакансии | [вакансии](вакансии/README.md) |
| POST | `/management/vacancies/ai/{vacancyId}` | Создание кандидата при помощи ИИ | [вакансии](вакансии/README.md) |
| GET | `/management/vacancies/{id}` | Получение информации о конкретной вакансии | [вакансии](вакансии/README.md) |
| PUT | `/management/vacancies/{id}` | Редактирование вакансии | [вакансии](вакансии/README.md) |
| POST | `/management/vacancies/{id}/candidates` | Создание кандидата | [вакансии](вакансии/README.md) |
| PUT | `/management/vacancies/{vacancyId}/candidates/{candidateId}` | Редактирование кандидата | [вакансии](вакансии/README.md) |
| GET | `/management/vacancies/{vacancyId}/history` | Получение истории изменений вакансии | [вакансии](вакансии/README.md) |
| GET | `/management/candidates` | Получение списка кандидатов | [кандидаты](кандидаты/README.md) |
| GET | `/management/candidates/{candidateId}` | Получение информации о конкретном кандидате | [кандидаты](кандидаты/README.md) |
| GET | `/management/candidates/{candidateId}/history` | Получение истории изменений кандидата | [кандидаты](кандидаты/README.md) |
| GET | `/management/candidates/{candidateId}/interview-results` | Получение информации с вопросами-ответами кандидата на интервью | [кандидаты](кандидаты/README.md) |
| PUT | `/management/candidates/{candidateId}/interview-results` | Импорт файла с вопросами-ответами кандидата на интервью | [кандидаты](кандидаты/README.md) |
| POST | `/management/candidates/{candidateId}/resume/convert` | Конвертация резюме | [кандидаты](кандидаты/README.md) |
| GET | `/management/appointments` | Получение информации о назначениях | [назначения](назначения/README.md) |
| POST | `/management/appointments` | Создание назначения | [назначения](назначения/README.md) |
| GET | `/management/appointments/employees/{id}` | Проверка наличия активных назначений у сотрудника по его ID | [назначения](назначения/README.md) |
| GET | `/management/appointments/report` | Экспорт списка назначений в Excel | [назначения](назначения/README.md) |
| GET | `/management/appointments/{appointmentId}/history` | Получение истории изменений назначения | [назначения](назначения/README.md) |
| GET | `/management/appointments/{id}` | Получение информации о назначении по его ID | [назначения](назначения/README.md) |
| PUT | `/management/appointments/{id}` | Редактирование назначения | [назначения](назначения/README.md) |
| GET | `/management/projects` | Получение списка всех проектов | [проекты](проекты/README.md) |
| GET | `/management/projects` | Получение информации о конкретном проекте | [проекты](проекты/README.md) |
| PATCH | `/management/projects` | Редактирование карточки проекта | [проекты](проекты/README.md) |
| POST | `/management/projects` | Создание проекта | [проекты](проекты/README.md) |
| GET | `/management/projects/{projectId}/history` | Получение истории изменений проекта | [проекты](проекты/README.md) |
| GET | `/management/roles` | Получение списка ролей с подролями | [роли](роли/README.md) |
| GET | `/management/employees` | Получение списка сотрудников | [сотрудники](сотрудники/README.md) |
| POST | `/management/employees` | Создание карточки сотрудника | [сотрудники](сотрудники/README.md) |
| GET | `/management/employees/report` | Экспорт списка сотрудников в Excel | [сотрудники](сотрудники/README.md) |
| GET | `/management/employees/{employeeId}/history` | Получение истории изменений сотрудника | [сотрудники](сотрудники/README.md) |
| GET | `/management/employees/{id}` | Получение информации о сотруднике | [сотрудники](сотрудники/README.md) |
| PUT | `/management/employees/{id}` | Изменение информации о сотруднике | [сотрудники](сотрудники/README.md) |
| POST | `/management/files` | Импорт резюме | [файлы](файлы/README.md) |

