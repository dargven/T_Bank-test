Таблица clients

| Поле       | Тип       | Описание               |
|------------|-----------|------------------------|
| client_id  | PK(int)   | Id клиента             |
| password   | varchar   | Пароль клиента хэш.    |
| name       | str       | Информация о клиенте   |
| email      | str       | Информация о клиенте   |
| created_at | timestamp | Дата создания записи   |
| updated_at | timestamp | Дата обновления записи |

Таблица payments

| Поле         | Тип       | Описание                                               |
|--------------|-----------|--------------------------------------------------------|
| payment_id   | PK(int)   | Id платежа                                             |
| client_id    | FK(int)   | Id клиента, внешний ключ, связанный с таблицей clients |
| amount       | int       | Сумма платежа                                          |
| payment_date | timestamp | Дата платежа                                           |
| status       | varchar   | Информация о платеже                                   |
| created_at   | timestamp | Дата создания записи                                   |
| updated_at   | timestamp | Дата обновления записи                                 |

Таблица auth_tokens

| Поле            | Тип         | Описание                                               |
|-----------------|-------------|--------------------------------------------------------|
| id              | PK(int)     | Внутренний id таблицы                                  |
| token_id        | UK(varchar) | Аутентификационный токен клиента                       |
| client_id       | FK(int)     | Id клиента, внешний ключ, связанный с таблицей clients |
| expiration_date | timestamp   | Дата окончания действия токена                         |

Таблица blocks

| Поле         | Тип       | Описание                                               |
|--------------|-----------|--------------------------------------------------------|
| block_id     | PK(int)   | Id блокировки                                          |
| client_id    | FK(int)   | Id клиента, внешний ключ, связанный с таблицей clients |
| reason       | varchar   | Причина блокировки                                     |
| description  | varchar   | Описание причины блокировки(дополнительное)            |
| blocked_by   | varchar   | Кто заблокировал: system, manual                       |
| status       | varchar   | Статус: active, removed                                |
| blocked_at   | timestamp | Время блокировки                                       |
| unblocked_by | varchar   | Кто разблокировал: system,manual                       |
| unblocked_at | timestamp | Когда разблокировали                                   |

таблица block_logs

| Поле         | Тип       | Описание                                                 |
|--------------|-----------|----------------------------------------------------------|
| log_id       | PK(int)   | Id лога                                                  |
| block_id     | FK(int)   | Id блокировки, внешний ключ, связанный с таблицей blocks |
| action       | varchar   | Выполненное действие(block,ublock)                       |
| performed_by | varchar   | Кем выполнено действие(admin,system)                     |
| timestamp    | timestamp | Время выполнения действия                                |
