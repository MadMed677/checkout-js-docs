# Yandex Checkout UI

UI библиотека, для отрисовки банковской карты на странице пользователя,
которая работает по API Yandex.CheckoutJS



## Инициализация

> Подключаем скрипт на страницу

```html
<script src="https://ya.ru/cdn/yandex-checkout-ui.min.js"></script>
```

Библиотека подключается **только** через CDN.
Чтобы подключить ее, нужно подключить скрипт из CDN, после этого в глобальной
области видимости библиотека будет доступна под именем **YandexCheckoutUI**



## Аудентификация

```js
const checkout = YandexCheckoutUI(123456);
```

> Где **123456** ваш секретный токен

Чтобы создать токен, вы должны авторизоваться к личном кабинете
[Яндекс.Касса](https://ya.ru). После этого перейти в раздел
создания токена для вашего магазина. Не в коем случае не выставляйте ваш
секретный токен на ружу! Это приватная информация, ни кто
не должен о нем знать кроме вас.

<aside class="warning">Не показывайте свой токен ни кому!</aside>

После этого вы можете создать инстанс от YandexCheckoutUI и использовать
**checkout** для генерации токена по данным банковской карты.



## Конфигурация

```js
const checkout = YandexCheckout(123456, {
    language: 'en',
    domSelector: '.my-selector'
});
```

Также вы можете передать второй аргумент, который будет отвечать за конфигурацию.

| Название параметра | Описание                               | Значение / Тип  | Значене по умолчанию |
| ------------------ | -------------------------------------- | --------------- | -------------------- |
| language           | язык ответов                           | 'en' / 'ru'     | 'ru'                 |
| domSelector        | селектор, куда будет отрендерена форма | string          | document.body        |
| amount             | стоимость                              | number          | 0                    |

> Возможные значения:

```js
{
    // язык вывода ответов
    language: string ('en' | 'ru') ['ru'],
    
    // селектор, куда будет отрендерена форма с оплатой
    domSelector: string ['document.body'],
    
    // стоимость, которую нужно показать на форме
    amount: string | number ['0']
}
```

## Публичный API

| Название метода | Описание               | Принимаемые значения     | Возвращаемые значения |
| --------------- | ---------------------- | ------------------------ | --------------------- |
| `.open`         | Открытие формы         |                          | {void}                |
| `.close`        | Закрытие формы         |                          | {void}                |
| `.on`           | Подписка на события    | 'yc_error', 'yc_success' | {void}                |

## `.open`

Открытие созданной формы.

```js
const checkout = YandexCheckoutUI(123456);

checkout.open();
```

## `.close`

Скрытие созданной формы

```js
checkout.close();
```

## `.on`

Подписка на события.
Есть 2 варианта, на событие ошибки `yc_error` или событие успеха `yc_success`.

| Название события | Описание                     | Возвращаемые значения |
| ---------------- | ---------------------------- | --------------------- |
| yc_error         | Произошла ошибка любого рода | [Объект, точно такого же вида, что и ошибка в Yandex.CheckoutJS](#yc-errors) |
| yc_success       | Токен успешно создан         | [Объект, точно такого же вида, что и успешный ответ в Yandex.CheckoutJS](#yc-success) |

> Пример с ошибкой

```js
checkout.on('yc_error', response => {
    /*
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
    */
    console.log(response);
});
```

> Пример с успехом

```js
checkout.on('yc_success', response => {
    /*
    {
        message: 'Токен для оплаты создан',
        status_code: 200,
        type: 'payment_token_created',
        response: {
            paymentToken: 'eyJlbmNyeXB0ZWRNZXNzYWdlIjoiWlc1amNubHdkR1ZrVFdWemMyRm5aUT09IiwiZXBoZW1lcmFsUHVibGljS2V5IjoiWlhCb1pXMWxjbUZzVUhWaWJHbGpTMlY1IiwidGFnIjoiYzJsbmJtRjBkWEpsIn0K'
        }
    }
    */
    console.log(response);
});
```
