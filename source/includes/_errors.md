# Ошибки


## Статус коды ошибок

> | Статус код ошибки | Значение |
> | ---------- | -------- |
> | 400        | Ошибка валидации банковской карты |
> | 401        | Ошибка аудентификации |
> | 402        | Ошибка подключения к API Яндекс.Кассы |

<aside class="notice">This error section is stored in a separate file in `includes/_errors.md`. Slate allows you to optionally separate out your docs into many files...just save them to the `includes` folder and add them to the top of your `index.md`'s frontmatter. Files are included in the order listed.</aside>

CheckoutJs поддерживает ошибки привычных HTTP запросов. Все коды, начинающиеся с `20*` сигнализируют об успешном платеже,
`40*` о том, что что-то пошло не так.


## Типы ошибок

> | Тип ошибки             | Значение  |
> | ---------------------- | --------- |
> | authentication_error   | Проблема с аудентификацией |
> | api_connection_error   | Не получилось установить соединение с Яндекс.Кассой |
> | api_error              | Произошла ошибка на стороне Яндекс.Кассы |
> | card_error             | Что-то не так с банковской карты |
> | invalid_request_error  | Неверные данные запроса |
> | validation_error       | Ошибка валидации, какое-то из полей карты введено не верно |


## Коды ошибок

> | Код ошибки | Значение |
> | ---------- | -------- |
> | invalid_number | Не валидный номер карты |
> | invalid_expiry_month | Не верный месяц истечения карты |
> | invalid_expiry_year | Не верный год истечения карты |
> | invalid_cvc | Не верный cvc/cvv код |
> | expired_card | Карта просрочена |
> | card_declined | Карта отклонена |
> | processing_error | Ошибка при проверке карты |
> | missing | Какая-то ошибка |
