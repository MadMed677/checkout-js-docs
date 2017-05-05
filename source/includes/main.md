# Yandex Checkout
[![Build Status](https://travis-ci.com/MadMed677/checkout-js.svg?token=JGyqoPse941Gzbw8Wg9k&branch=master)](https://travis-ci.com/MadMed677/checkout-js) [![codecov](https://codecov.io/gh/MadMed677/checkout-js/branch/master/graph/badge.svg?token=kREGja9bnJ)](https://codecov.io/gh/MadMed677/checkout-js) [![github tags](https://img.shields.io/github/tag/MadMed677/checkout-js.svg?style=flat-square)](https://github.com/MadMed677/checkout-js/tags)

Библиотека для токенизации банковской карты на стороне Яндекс.Денег.



# Инициализация

> Подключаем скрипт на страницу

```html
<script src="https://ya.ru/cdn/yandex-checkout.min.js"></script>
```

Библиотека подключается только через CDN.
Чтобы подключить ее, нужно подключить скрипт из CDN, после этого в глобальной области видимости библиотека будет доступна
под именем **CheckoutJs**



# Аудентификация

```js
const checkout = YandexCheckout(123456);
```

> Где **123456** ваш секретный токен

Чтобы создать токен, вы должны авторизоваться к личном кабинете [Яндекс.Касса](https://ya.ru). После этого перейти в раздел
создания токена для вашего магазина. Не в коем случае не выставляйте ваш секретный токен на ружу! Это приватная информация, ни кто
не должен о нем знать кроме вас.

После этого вы можете создать инстанс от YandexCheckout и использовать **checkout** для генерации токена по данным банковской карты.



# Конфигурация

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
