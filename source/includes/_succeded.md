## Токенизация

> Формат выдачи успешно запроса

```js
{
    type: string,
    message: ?string,
    status_code: number,
    response: object
}
```

> Пример. Токен успешно получен

```js
{
    message: 'Токен для оплаты создан',
    status_code: 200,
    type: 'payment_token_created',
    response: {
        paymentToken: 'eyJlbmNyeXB0ZWRNZXNzYWdlIjoiWlc1amNubHdkR1ZrVFdWemMyRm5aUT09IiwiZXBoZW1lcmFsUHVibGljS2V5IjoiWlhCb1pXMWxjbUZzVUhWaWJHbGpTMlY1IiwidGFnIjoiYzJsbmJtRjBkWEpsIn0K'
    }
}
```

### Статус коды успеха

| Статус код | Значение             |
| ---------- | -------------------- |
| 200        | Токен успешно создан |
| 202        | Запрос принят к обработке, но результат его обработки еще неизвестен |

### Типы

| Тип                    | Значение  |
| ---------------------- | --------- |
| payment_token_created  | Токен успешно создан |

