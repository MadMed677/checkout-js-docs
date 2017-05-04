# Yandex.Money CheckoutJS
[![Build Status](https://travis-ci.com/MadMed677/checkout-js.svg?token=JGyqoPse941Gzbw8Wg9k&branch=master)](https://travis-ci.com/MadMed677/checkout-js) [![codecov](https://codecov.io/gh/MadMed677/checkout-js/branch/master/graph/badge.svg?token=kREGja9bnJ)](https://codecov.io/gh/MadMed677/checkout-js) [![github tags](https://img.shields.io/github/tag/MadMed677/checkout-js.svg?style=flat-square)](https://github.com/MadMed677/checkout-js/tags)

Библиотека для токенизации банковской карты на стороне Яндекс.Денег.



# Инициализация

> Подключаем скрипт на страницу

```html
<script src="https://ya.ru/cdn/yandex-checkout-js.min.js"></script>
```

Просто какой-то текст

# Создания токена

## Get All Kittens

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve
