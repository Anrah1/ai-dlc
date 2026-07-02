# Экспорт списка назначений в Excel

**GET** `/management/appointments/report`

Выгрузка списка проектов в Excel
**Описание метода:**
Метод предназначен для выгрузки списка всех назначений в Excel файл.
**Логика выполнения метода:**
Сервер обращается к DB planer scheme planer для получения информации, соответствующей условиям запроса.
После извлечения данные генерируются в Excel файл.
Сервер в теле ответа передает закодированный поток данных (байтовый поток), который в браузере дешифруется в ссылку на скачивание файла, в заголовке ответа указывает название файла.
Браузер автоматически скачивает этот файл.
Метод: GET
Эндпоинт: /management/appointments/report
**Строка**** запроса****: **GET /management/appointments/report
**Ответ: **Зашифрованный поток данных, в котором содержится сгенерированный файл "appointments report at DD-MM-YYYY.xlsx"
**Данные таблицы:**

| Поле | Мэппинг на БД |
| --- | --- |
| Сотрудник | planer.employees.last_name + " " + planer.employees.first_name |
| Роль | planer.roles.name |
| Подроль | planer.subroles.name |
| Грейд | planer.appointments.grade |
| Тип сотрудника | planer.employees.type |
| Руководитель | planer.employees.external_manager (если planer.employees.type = external) or leader: planer.employees.last_name + planer.employees.first_name (если planer.employees.type = internal) |
| Проект | planer.projects.name |
| Заказчики | planer.appointments.customers |
| Ответственный за обратную связь | planer.appointments.responsible_for_feedback |
| Дата подключения | planer.appointments.start_date |
| Дата отключения | planer.appointments.end_date |
| Условия | planer.appointments.condition |
| Ставка без НДС | planer.appointments.rate_no_nds + "₽" |
| Процент с ЧК | planer.appointments.percent + "%" |
| Даты оплаты | planer.payment_dates.date |
| Условия по ЧК | planer.charge_codes.from_charge_code + " →" + planer.charge_codes.to_charge_code + "~" + planer.charge_codes.type |
| Партнер | planer.appointments.partner |
| Ставка у партнера | planer.appointments.rate_partner |
| Статус | planer.appointments.status |
| Комментарий | planer.appointments.comment |

**Шаблон таблицы:**

| Сотрудник | Роль | Подроль | Грейд | Тип сотрудника | Руководитель | Проект | Заказчики | Ответственный за обратную связь | Дата подключения | Дата отключения | Условия | Ставка без НДС | Процент с ЧК | Даты оплаты | Условия по ЧК | Партнер | Ставка у партнера | Статус | Комментарий |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Костина Анфиса | Аналитик | Системный | Senior | Внутренний | Папкин Роман | Автоматизация Решелье | Рогов | Петров | 05.01.2025 | 05.01.2026 | Профитшеринг | 2000 ₽ |  | 10.06.2025; / 10.01.2026 | CRM_SBS_N_SB_CORP_CKR123456666 50% -> CRM_RSB_N_SB_CORPCKR1622727
7191 ~ Доход;
CRM_RSB_N_TELE2_TDSOS -> INV_OCS_N_TELE2_TDSOS ~ Расход |  |  | Активно | Комментарий |

**Пример успешного ответа**
200 ОК

###### Методы для работы с проектами
