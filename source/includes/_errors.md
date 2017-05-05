# Ошибки

> Статусы ошибок

> Код ошибки | Значение | Описание |
> ---------- | -------- | -------- |
> 400        | Ошибка валидации банковской карты | |
> 401        | Ошибка аудентификации | |
> 402        | Ошибка подключения к API Яндекс.Кассы | |

<aside class="notice">This error section is stored in a separate file in `includes/_errors.md`. Slate allows you to optionally separate out your docs into many files...just save them to the `includes` folder and add them to the top of your `index.md`'s frontmatter. Files are included in the order listed.</aside>

CheckoutJs поддерживает ошибки привычных HTTP запросов. Все коды, начинающиеся с `20*` сигнализируют об успешном платеже,
`40*` о том, что что-то пошло не так.
