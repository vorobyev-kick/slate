---
title: Ex API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>
  - <a href='index_ru.html'>Описание API на русском языке</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the External API.


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
This section covers methods that provide data regarding available currencies and currency pairs and rates.
<aside class="notice">
You don't need to authorize to use methods from <b>Market</b> section.
</aside>


## Pairs

```shell
curl "http://example.com/api/v1/market/pairs?type=market"
```

> The above command returns JSON structured like this:

```json
{
	"pairId": 111111111,
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

### HTTP Request

`GET https://example.com/api/v1/market/pairs?type=market`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
type | string | Yes | Currently the only valid value is 'market'

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairId | integer | Yes | Currency pair unique identifier 
pairName | string | Yes | Currency pair name *(ex: BTC/USDT)*
baseCurrency | string | Yes | Base currency name *(ex: BTC)*
quoteCurrencу | string | Yes | Quotes currency name *(ex: USDT)*
baseMinSIze | string | Yes | Minimum amount of base currency for order creation
quoteMinSize | string | Yes | Minimum amount of quote currency for order creation
priceDecimal | Number | Yes | Price fraction digits 
amountDecimal | Number | Yes | Amount fraction digits
feeTaker | string | Yes | Taker fee (percentage of transaction amount)
feeMaker | string | Yes | Maker fee (percentage of transaction amount)
isFrozen | integer | Yes | Attribute showing if trading on this currency pair is frozen or not: <br/>0 – trading is available <br/>1 – traiding is unavailable

## Ticker

```shell
curl "http://example.com/api/v1/market/ticker?pairName=BTC/USDT"
```

> The above command returns JSON structured like this:

```json
{
	"pairId": 111111111,
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

### HTTP Request

`GET https://example.com/api/v1/market/ticker?pairName=BTC/USDT`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string | Yes | Currency pair name *(ex: BTC/USDT)*

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairId | integer | Yes | Currency pair unique identifier 
pairName | string | Yes | Currency pair name *(ex: BTC/USDT)*
bestBid | string | Yes | Best bid
bestAsk | string | Yes | Best ask
lastPrice | string | Yes | Last deal price
lastVolume | string | Yes | Last deal volume
bestAskSize | string | Yes | Amount of currency in best ask
bestBidSize | string | Yes | Amount of currency in best bid
time | timestamp | Yes | Timestamp (milliseconds)

## All Tickers

**Description not finalized.**

## 24hrs stats

The method provides statistics on a currency pair during the last 24 hours.

```shell
curl "http://example.com/api/v1/market/stats24?pairName=BTC/USDT"
```

> The above command returns JSON structured like this:

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

### HTTP Request

`GET https://example.com/api/v1/market/stats24?pairName=BTC/USDT`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string | Yes | Currency pair name *(ex: BTC/USDT)*

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string | Yes | Currency pair name *(ex: BTC/USDT)*
high24 | string | Yes | Maximum price during last 24 hours
low24 | string | Yes | Minimum price during last 24 hours
amountVol | string | Yes | Aggregated deals volume during last 24 hours
baseVol | string | Yes | Aggregated deals volume during last 24 hours in base currency
lastPrice | string | Yes | Last deal price
bestBid | string | Yes | Best bid price
bestAsk | string | Yes | Best ask price
averagePrice | string | Yes | Average price during last 24 hours
priceChange | string | Yes | Price change during last 24 hours
time | timestamp | Yes | Timestamp
changeRate? | string | Yes | 

## Currency

The method provides data regarding specified currency. If *currency* parameter is not provided, returns data regarding all available currencies.

```shell
curl "http://example.com/api/v1/currencies?currency=ETH"
```

> The above command returns JSON structured like this:

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

### HTTP Request

`GET https://example.com/api/v1/currencies?currency=ETH`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
currency | string | Yes | Currency short name *(ex: BTC)*

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
currencyCode | string | ? | Currency short name
currencyName | string | Yes | Currency short name
fullName | string | Yes | Currency full name
decimal | number | Yes | Currency fraction digits
minWithdawal | string | ? | Minimum withdrawal amount
minFeeWithrawal? | string | ? | Minimum withdrawal fee
isWithdrawEnable | integer | ? | Is withdrawal available?
isDepositEnable | integer | ? | Is deposit available?
isExchangeEnable | integer | ? | Is exhange available?
isFrozen | integer | ? | Is frozen?

## Orderbook

## Trade history

## Currencies

# Trade 

This section covers methods that operate with exchange orders.

<aside class="warning">
Authorization is needed to use these methods.
</aside>

## Place Order 

установка ордера

## Cancel Order 

отмена ордера

## Cancel All Orders

отмена группы ордеров или всех ордеров

## Active Orders List 

получение информации об активных ордерах

## Orders List 

получение информации о завершенных ордерах

## Trade List 

получение информации об истории сделок Пользователя

# User 

набор методов информации о Пользователе и его аккаунте на криптовалютной бирже (требуется авторизация)

<aside class="warning">
Authorization is needed to use these methods.
</aside>


## User Info 

информация об аккаунте

## Balance

информация о балансе Пользователя;

## Deposit Address 

получение адреса для Пополнения

## Deposit History 

история пополнений

## Withdraw 

осуществление вывода средств;

## Withdraw History 

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

