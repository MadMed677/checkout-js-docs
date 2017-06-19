# Yandex Checkout UI

UI библиотека, для отрисовки банковской карты на странице пользователя,
которая работает по API Yandex.CheckoutJS



## Инициализация

> Подключаем скрипт на страницу

```html
<script src="https://static.yandex.net/checkout-ui/yandex-checkout-ui.js"></script>
```

Библиотека подключается **только** через CDN.
Чтобы подключить ее, нужно подключить скрипт из CDN, после этого в глобальной
области видимости библиотека будет доступна под именем **YandexCheckoutUI**



## Аудентификация

```js
const $checkout = YandexCheckoutUI(123456);
```

> Где **123456** ваш `merchant_id`

Чтобы создать токен, вы должны авторизоваться к личном кабинете
[Яндекс.Касса](https://kassa.yandex.ru). После этого перейти в раздел
создания токена для вашего магазина. Не в коем случае не выставляйте ваш
секретный токен на ружу! Это приватная информация, ни кто
не должен о нем знать кроме вас.

После этого вы можете создать инстанс от YandexCheckoutUI и использовать
**$checkout** для генерации токена по данным банковской карты.



## Конфигурация

```js
const $checkout = YandexCheckoutUI(123456, {
    language: 'en',
    domSelector: '.my-selector',
    amount: 99.99
});
```

Также вы можете передать второй аргумент, который будет отвечать за конфигурацию.

| Название параметра | Описание                               | Значение / Тип  | Значене по умолчанию |
| ------------------ | -------------------------------------- | --------------- | -------------------- |
| language           | язык ответов                           | 'en' / 'ru'     | 'ru'                 |
| amount             | стоимость                              | number          | 0                    |
| isRecurrent        | отрисовать на форме сообщение о том, что будут производиться рекуррентные платежи  | boolean          | false                    |

> Возможные значения:

```js
{
    // язык вывода ответов
    language: string ('en' | 'ru') ['ru'],

    // стоимость, которую нужно показать на форме
    amount: number ['0'],

    // Будут производиться реруррентные платежи
    isRecurrent: true [false]
}
```

## Публичный API

| Название метода      | Описание                            | Принимаемые значения     | Возвращаемые значения |
| ---------------      | ----------------------------------- | ------------------------ | --------------------- |
| `.open`              | Открытие формы                      |                          | {void}                |
| `.close`             | Закрытие формы                      |                          | {void}                |
| `.on`                | Подписка на события                 | 'yc_error', 'yc_success' | {void}                |
| `.showLantern`       | Показать фонарь                     | text {string}            | {void}                |
| `.hideLantern`       | Скрыть фонарь                       |                          | {void}                |
| `.showLantern`       | Переключает состояние фонаря        | text {string}            | {void}                |
| `.chargeSuccessful`  | Успешный ответ от APIv3             | text {string}            | {void}                |
| `.chargeFailful`     | Ошибка от APIv3                     | text {string}            | {void}                |

## `.open`

Открытие формы.

```js
const $checkout = YandexCheckoutUI(123456);
$checkout.open();
```

## `.close`

Скрытие формы

```js
const $checkout = YandexCheckoutUI(123456);
$checkout.close();
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
$checkout.on('yc_error', response => {
    /*
    {
        status: 'error',
        error: {
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
    }
    */
});
```

> Пример с успехом

```js
$checkout.on('yc_success', response => {
    /*
    {
        status: 'success',
        data: {
            message: 'Токен для оплаты создан',
            status_code: 200,
            type: 'payment_token_created',
            response: {
                paymentToken: 'eyJlbmNyeXB0ZWRNZXNzYWdlIjoiWlc1amNubHdkR1ZrVFdWemMyRm5aUT09IiwiZXBoZW1lcmFsUHVibGljS2V5IjoiWlhCb1pXMWxjbUZzVUhWaWJHbGpTMlY1IiwidGFnIjoiYzJsbmJtRjBkWEpsIn0K'
            }
        }
    }
    */
    console.log(response);
});
```

## `showLantern`

Показать фонарь с ошибкой над формой (если произошла какая-нибудь ошибка при запросе на backend)

| Название параметра | Тип    | Описание     |
| text               | string | Текст ошибки |

```js
const $checkout = YandexCheckoutUI(123456);
$checkout.showLantern('Текст ошибки');
```

## `hideLantern`

Скрыть фонарь с ошибкой

```js
const $checkout = YandexCheckout(123456);
$checkout.hideLantern();
```

## `toggleLantern`

Открывает/скрывает фонарь с ошибкой

| Название параметра | Тип    | Описание     |
| text               | string | Текст ошибки |

```js
const $checkout = YandexCheckoutUI(123456);
$checkout.toggleLantern('Текст ошибки');
```

## `chargeSuccessful`

Ответ от APIv3 успешен. После вызова данного метода, будет закрыт фонарь (если тот открыт)
после этого закроется форма.

```js
const $checkout = YandexCheckoutUI(123456);

// открываем форму
$checkout.open();

// Токен успешно сгенерирован
$checkout.on('yc_success', () => {
    // запрос на бэкенд
    // ...

    // Если оплата прошла успешно, то вызываем метод
    $checkout.chargeSuccessful();
});
```

## `chargeFailful`

Ответ от APIv3 не успешен. После вызова данного метода будет открыт фонарь с ошибкой.

| Название параметра | Тип    | Описание     |
| text               | string | Текст ошибки |

```js
const $checkout = YandexCheckoutUI(123456);

// открываем форму
$checkout.open();

// Токен успешно создан
$checkout.on('yc_success', () => {
    // запрос на бэкенд
    // ...

    // Оплата не прошла
    $checkout.chargeFailful();
});
```
