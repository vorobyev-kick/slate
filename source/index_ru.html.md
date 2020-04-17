---
title: Описание внешнего API

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>
  - <a href='index.html'>API documentation in English</a>

includes:
  - errors

search: true
---

# Ведение

API для внешней интеграции


# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Market
Данный раздел описывает набор методов, передающих информацию о парах и криптовалютах на платформе.
<aside class="notice">
Методы раздела <b>Market</b> доступны без авторизации.
</aside>


## Pairs

```shell
curl "http://example.com/api/v1/market/pairs?type=market"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"pairName": "BTC/USDT",
	"baseCurrency": "BTC",
	"quoteCurrencу": "USDT",
	"baseMinSIze": "0.0001",
	"quoteMinSize": "0.0001",
	"priceDecimal": 12,
	"amountDecimal": 8,
	"feeTaker": "0.15",
	"feeMaker": "0.15",
	"isFrozen": 0
}
```

### HTTP Запрос

`GET https://example.com/api/v1/market/pairs?type=market`

### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
type | string | Да | Единственное корректное значение - 'market'

### Параметры ответа
Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | наименование криптовалютной пары *(пример: BTC/USDT)*
baseCurrency | string | Да | наименование базовой криптовалюты *(пример: BTC)*
quoteCurrencу | string | Да | наименование котируемой криптовалюты *(пример: USDT)*
baseMinSIze | string | Да | минимальное кол-во базовой криптовалюты для выставления ордера
quoteMinSize | string | Да | минимальное количество котируемой криптовалюты для выставления ордера
priceDecimal | Number | Да | максимальное количество знаков после точки для пары при указании цены
amountDecimal | Number | Да | максимальное количество знаков после точки для пары при указании количества
feeTaker | string | Да | комиссия тэйкера (процент от суммы сделки)
feeMaker | string | Да | комиссия мэйкера (процент от суммы сделки)
isFrozen | integer | Да | Индикатор, показывающий, доступна ли торговля по паре (0 – доступна) 1 – не доступна

## Ticker

```shell
curl "http://example.com/api/v1/market/ticker?pairName=BTC/USDT"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"pairName": "BTC/USDT",
	"bestBid": "BTC",
	"bestAsk": "USDT",
	"lastPrice": "0.0001",
	"lastVolume": "0.0001",
	"bestAskSize": 12,
	"bestBidSize": 8,
	"time": "0.15"
}
```

### HTTP Запрос

`GET https://example.com/api/v1/market/ticker?pairName=BTC/USDT`

### Параметры URL

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | Имя криптовалютной пары *(пример: BTC/USDT)*

### Параметры ответа
Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | Наименование криптовалютной пары *(пример: BTC/USDT)*
bestBid | string | Да | Лучший бид
bestAsk | string | Да | Лучший аск
lastPrice | string | Да | Последняя цена сделки
lastVolume | string | Да | Последний объем сделки
bestAskSize | string | Да | Количество криптовалюты по цене лучшего аска
bestBidSize | string | Да | Количество криптовалюты по цене лучшего бида
time | timestamp | Да | Время, на которое получены данные (в миллисекундах)

## All Tickers

**Описание ещё не завершено**

## 24hrs stats

Метод возвращает данные по криптовалютной паре за последние 24 часа.

```shell
curl "http://example.com/api/v1/market/stats24?pairName=BTC/USDT"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"pairName": 111111111,
	"high24": "BTC/USDT",
	"low24": "BTC",
	"amountVol": "USDT",
	"baseVol": "0.0001",
	"lastPrice": "0.0001",
	"bestBid": 12,
	"bestAsk": 8,
	"averagePrice": "0.15",
	"priceChange": 111111111,
	"time": "BTC/USDT",
	"changeRate?": "BTC"
}
```

### HTTP Запрос

`GET https://example.com/api/v1/market/stats24?pairName=BTC/USDT`

### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | Имя криптовалютной пары *(пример: BTC/USDT)*

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | наименование криптовалютной пары (В формате BTC/USDT)
high24 | string | Да | Наивысшая цена за 24 часа
low24 | string | Да | наименьшая цена за 24 чкаса
amountVol | string | Да | Количество криптовалюты, задействованной в сделках за 24 часа
baseVol | string | Да | Объем торгов за 24 часа выраженный в базовой криптовалюте
lastPrice | string | Да | последняя цена сделки в паре
bestBid | string | Да | лучшая цена на покупку
bestAsk | string | Да | лучшая цена на продажу
averagePrice | string | Да | средняя цена в сделках за 24 часа
priceChange | string | Да | Изменение цены за 24 часа
time | timestamp | Да | Время, на которое действительна полученная информация в миллисекундах
changeRate? | string | Да | 

## Currency

В случае, если параметр в запросе не отправлен, предоставляется информация по всем криптовалютам платформы.

```shell
curl "http://example.com/api/v1/currencies?currency=ETH"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"currencyCode": 111111111,
	"currencyName": 111111111,
	"fullName": 111111111,
	"decimal": 111111111,
	"minWithdawal": 111111111,
	"minFeeWithrawal?": 111111111,
	"isWithdrawEnable": 111111111,
	"isDepositEnable": 111111111,
	"isExchangeEnable": 111111111,
	"isFrozen": 111111111
}
```

### HTTP Запрос

`GET https://example.com/api/v1/currencies?currency=ETH`

### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
currency | string | Нет | Краткое наименование криптовалюты (токена) *(пример: BTC)*

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
currencyCode | string | ? | краткое наименование криптовалюты по ISO4217
currencyName | string | Да | краткое наименование криптовалюты
fullName | string | Да | полное наименование криптовалюты
decimal | number | Да | Количество знаков после точки для этой криптовалюты
minWithdawal | string | ? | минимальное количество криптовалюты, которое разрешено выводить с платформы
minFeeWithrawal? | string | ? | минимальный размер комиссии взимаемый за вывод средств
isWithdrawEnable | integer | ? | Индикатор, показывающий, доступен ли вывод (0 – доступен) 1 – не доступен
isDepositEnable | integer | ? | Индикатор, показывающий, доступно ли пополнение (0 – доступно) 1 – не доступно
isExchangeEnable | integer | ? | Индикатор, показывающий, доступен ли обмен на платформе этой криптовалюты (0 – доступно) 1 – не доступно
isFrozen | integer | ? | Индикатор, показывающий, доступна ли торговля этой криптовалюты на бирже (0 – доступна) 1 – не доступна

## Orderbook

## Trade history



# Trade 

Набор методов для выставления ордеров и получения информации об ордерах.

<aside class="warning">
Для использования данных методов требуется авторизация.
</aside>


## place order 

установка ордера

## cancel order 

отмена ордера

## cancel all orders 

отмена группы ордеров или всех ордеров

## active orders list 

получение информации об активных ордерах

## orders list 

получение информации о завершенных ордерах

## trade list 

получение информации об истории сделок Пользователя

# User 

набор методов информации о Пользователе и его аккаунте на криптовалютной бирже 

<aside class="warning">
Для использования данных методов требуется авторизация.
</aside>

## userinfo 

информация об аккаунте

## balance

информация о балансе Пользователя;

## depositaddress 

получение адреса для Пополнения

## deposit history 

история пополнений

## withdraw 

осуществление вывода средств;

## withdrawhistory 

история вывода средств;

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

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

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

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

