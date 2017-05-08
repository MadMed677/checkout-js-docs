## <a name="yc-errors">Ошибки</a>

> Формат выдачи ошибок

```js
{
    type: string,
    message: ?string,
    status_code: number,
    code: ?string,
    params: Array<object>
}
```

> Пример 1. Произошла ошибка в подключении к серверу

```js
{
    type: 'api_connection_error',
    message: 'Ошибка в подключении сервера',
    status_code: 402,
    code: 'processing_error',
    params: []
}
```


> Пример 2. Произошла ошибка валидации

```js
{
    type: 'validation_error',
    message: undefined,
    status_code: 400,
    code: undefined,
    params: [
        {
            code: 'invalid_number',
            message: 'Неверный номер карты'
        },
        {
            code: 'invalid_expiry_month',
            message: 'Невалидное значение месяца'
        }
    ]
}
```

### Статус коды ошибок

| Статус код | Значение |
| ---------- | -------- |
| 400        | Ошибка валидации |
| 401        | Ошибка аудентификации |
| 402        | Ошибка подключения к API Яндекс.Кассы |


CheckoutJs поддерживает ошибки привычных HTTP запросов. Все коды, начинающиеся с `20*` сигнализируют об успешном платеже,
`40*` о том, что что-то пошло не так.


### Типы ошибок

| Тип ошибки             | Значение  |
| ---------------------- | --------- |
| authentication_error   | Проблема с аудентификацией |
| api_connection_error   | Не получилось установить соединение с Яндекс.Кассой |
| api_error              | Произошла ошибка на стороне Яндекс.Кассы |
| card_error             | Что-то не так с банковской карты |
| invalid_request_error  | Неверные данные запроса |
| validation_error       | Ошибка валидации, какое-то из полей карты введено не верно |


### Коды ошибок

| Код ошибки | Значение |
| ---------- | -------- |
| invalid_number | Не валидный номер карты |
| invalid_expiry_month | Не верный месяц истечения карты |
| invalid_expiry_year | Не верный год истечения карты |
| invalid_cvc | Не верный cvc/cvv код |
| expired_card | Карта просрочена |
| card_declined | Карта отклонена |
| processing_error | Ошибка при проверке карты |
| missing | Какая-то ошибка |

