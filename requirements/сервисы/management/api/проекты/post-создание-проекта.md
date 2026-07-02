# Создание проекта

**POST** `/management/projects`

Создание проекта
**Описание метода:**
Метод предназначен для создания нового проекта
Метод: POST
Эндпоинт: https://management/projects
**Строка**** запроса****: **POST  https://management/projects

| **Название параметра** | **Тип данных** | **Обязательность** | **Описание** | **Мэппинг на БД** |
| --- | --- | --- | --- | --- |
| name | string / (формат: integer($int64)) | + | Название проекта | planer.projects.name |
| managerId | number / (формат: integer($int64)) | + | Идентификатор менеджера | planer.projects.manager_id |
| type | string / (формат: enum) | + | Тип проекта / enum (Внутренний/внешний) | planer.projects.type |
| chargeCode | string | - | Список Кодов проекта (ЧК). В БД хранится  строкой с разделителем ";" | planer.projects.charge_code |
| comment | string | - | Комментарий к проекту | planer.projects.comment |
| status | string / (формат: enum) | + | Статус ACTIVE проставляется с фронта | planer.projects.status |

status приходит с фронта
** Пример**** запроса****:**

| { / "name": "Планер", / "managerId": 11, / "type": "INTERNAL", / "chargeCode": "CRM_123123123", / "comment": "комментарий", / "status": "ACTIVE" / } |
| --- |

**Пример успешного ответа**
201 Created: Проект успешно создан
**Тело ответа:**

| { / "id": 12345, / "name": "Планер", / "manager": { / "managerId": 11, / "lastName": "Петров", / "firstName": "Петр", / "middleName": "Петрович", / "role": "MANAGER", / "grade": "LEAD_EXPERT", / "leader": **null**, / "externalManager": "string", / "managerContact": "string", / "birthDate": "string", / "comment": "string", / "type": "INTERNAL", / "status": "ACTIVE" / }, / "type": "INTERNAL", / "chargeCode": "CRM_123123123", / "status": "ACTIVE", / "comment": "комментарий" / } |
| --- |

**Примеры ответов в случае ошибки**
- 400 Bad Request: Некорректные данные запроса
*сервер не может обработать запрос из-за неверного синтаксиса. Это может быть связано с отсутствующими обязательными полями  или неверным форматом данных.
тело ответа

| { / "timestamp": "2024-12-19T10:04:37.345+00:00", / "status": "400", / "error": "Bad Request", / "path": "/management/projects" / } |
| --- |

404 Not Found: Менеджер не найден

| { / "message": "Сотрудник (менеджер) с идентификатором '100' не найден." / } |
| --- |

409 Conflict: Конфликт из-за попытки создать дублирующий проект
*Например, если проект с таким же названием уже существует.

| { / "message": "Проект с названием 'Проект А' уже существует." / } |
| --- |

**Валидации **
При получении запроса сервис проводит валидацию данных
Проверка заполнения всех обязательных полей (name, manager_id, type)
Проверка уникальности названия проекта. иначе ошибка "409"
Проверка наличия менеджера: если менеджер не найден ошибка "404
