# Yandex Checkout JS
[![Build Status](https://travis-ci.com/MadMed677/checkout-js.svg?token=JGyqoPse941Gzbw8Wg9k&branch=master)](https://travis-ci.com/MadMed677/checkout-js) [![codecov](https://codecov.io/gh/MadMed677/checkout-js/branch/master/graph/badge.svg?token=kREGja9bnJ)](https://codecov.io/gh/MadMed677/checkout-js) [![github tags](https://img.shields.io/github/tag/MadMed677/checkout-js.svg?style=flat-square)](https://github.com/MadMed677/checkout-js/tags)

Библиотека для токенизации банковской карты на стороне Яндекс.Денег.



## <a name="yc-initialize">Инициализация</a>

> Подключаем скрипт на страницу

```html
<script src="https://ya.ru/cdn/yandex-checkout.min.js"></script>
```

Библиотека подключается только через CDN.
Чтобы подключить ее, нужно подключить скрипт из CDN, после этого в глобальной
области видимости библиотека будет доступна под именем **YandexCheckout**



## <a name="yc-authentication">Аудентификация</a>

```js
const checkout = YandexCheckout(123456);
```

> Где **123456** ваш секретный токен

Чтобы создать токен, вы должны авторизоваться к личном кабинете [Яндекс.Касса](https://ya.ru). После этого перейти в раздел
создания токена для вашего магазина. Не в коем случае не выставляйте ваш секретный токен наружу! Это приватная информация, ни кто
не должен о нем знать кроме вас.

После этого вы можете создать инстанс от YandexCheckout и использовать **checkout** для генерации токена по данным банковской карты.



## <a name="yc-configuration">Конфигурация</a>

```js
const checkout = YandexCheckout(123456, {
    language: 'en'
});
```

Также вы можете передать второй аргумент, который будет отвечать за конфигурацию.

> Возможные значения:

```js
{
    // язык вывода ответов
    language: string ('en' | 'ru') ['ru']
}
```

## <a name="yc-public-api">Публичный API</a>

| Название метода | Описание               | Возвращаемые значения |
| --------------- | ---------------------- | --------------------- |
| `.generate`     | Генерация токена       | Promise{Object}       |
| `.validate`     | Валидация данных карты | {Object} / Boolean    |

## `.generate`

Используется для генерации токена.

```js
checkout.generate({
    number: '4444 4444 4444 4448',
    cvc: '123',
    month: '11',
    year: '20'
});
```

Параметры метода

| Название параметра  | Описание                                 | Тип      | Валидация                        |
| ------------------- | ---------------------------------------- | -------- | -------------------------------- |
| `number*`           | Номер банковской карты                   | {String} | Только числа. Длина 16 символов  |
| `fio`               | Имя владельца карты                      | {String} |                                  |
| `cvc*`              | 3 или 4 значный код на обратной стороне  | {String} | Только числа. Длина 3, 4 символа |
| `month*`            | Месяц истечения карты                    | {String} | Только числа. Длина 2 символа    |
| `year*`             | Год истечения карты                      | {String} | Только числа. Длина 2 символа    |


> Пример валидных данных:

```js
checkout.generate({
    number: '4444 4444 4444 4448',
    cvc: '123',
    month: '11',
    year: '20'
})
    .then(response => {
        if (response.status_code === 200) {
            const { paymentToken } = response;

            // eyJlbmNyeXB0ZWRNZXNzYWdlIjoiWlc...
            return paymentToken;
        }
    });
```

> Пример не валидных данных:

```js
checkout.generate({
    number: '4444 4444 4444 4441',
    cvc: '12',
    month: '12',
    year: '20'
})
    .catch(response => {
        if (response.status_code === 400) {
            // validation_error
            const type = response.type;

            /*
                [
                    {
                        code: 'invalid_expiry_month',
                        message: 'Невалидное значение месяца'
                    },
                    {
                        code: 'invalid_cvc',
                        message: 'Невалидное значение CVC'
                    }
                ]
            */
            // За большими подробностями ошибок смотрите в секцию ошибок
            const params = response.params;

            return response;
        }
    });
```
