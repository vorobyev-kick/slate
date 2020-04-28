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
	"pairs": [
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
		},
		{
			"pairName": "BTC/KICK",
			"baseCurrency": "BTC",
			"quoteCurrencу": "KICK",
			"baseMinSIze": "0.0001",
			"quoteMinSize": "0.0001",
			"priceDecimal": 12,
			"amountDecimal": 8,
			"feeTaker": "0.15",
			"feeMaker": "0.15",
			"isFrozen": 0
		}
	]
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
isFrozen | integer | Да | Индикатор, показывающий, доступна ли торговля по паре (0 – доступна, 1 – недоступна)

## Ticker

```shell
curl "http://example.com/api/v1/market/ticker?pairName=BTC/USDT"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"pairName": "BTC/USDT",
	"bestBid": "1234.1231",
	"bestAsk": "1245.2847",
	"lastPrice": "1242.1984",
	"lastVolume": "100000",
	"bestAskSize": "124990",
	"bestBidSize": "95830",
	"time": 1588024908
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
	"pairName": "BTC/USDT",
	"high24": "3425.0092",
	"low24": "3389.1294",
	"amountVol": "91572919",
	"baseVol": "27020.6311",
	"lastPrice": "3421.7623",
	"bestBid": "3420.4223",
	"bestAsk": "3401.7623",
	"averagePrice": "3407.3719",
	"priceChange": "36.0925",
	"time": 1588024908,
	"changeRate?": ""
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
	"currencyCode???": "KICK",
	"currencyName": "KICK",
	"fullName": "Kick Token",
	"decimal": 8,
	"minWithdawal???": "1",
	"minFeeWithrawal???": "0.1",
	"isWithdrawEnable???": 1,
	"isDepositEnable???": 1,
	"isExchangeEnable???": 1,
	"isFrozen???": 0
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
isWithdrawEnable | integer | ? | Индикатор, показывающий, доступен ли вывод (0 – доступен, 1 – недоступен)
isDepositEnable | integer | ? | Индикатор, показывающий, доступно ли пополнение (0 – доступно, 1 – недоступно)
isExchangeEnable | integer | ? | Индикатор, показывающий, доступен ли обмен на платформе этой криптовалюты (0 – доступно, 1 – недоступно)
isFrozen | integer | ? | Индикатор, показывающий, доступна ли торговля этой криптовалюты на бирже (0 – доступна, 1 – недоступна)

## Trades

Запрос истории сделок по конкретной паре за последние 24 часа.

```shell
curl "http://example.com/api/v1/market/trades?pairName=BTC/USDT&type=buy"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"tradeId": 111111111,
	"price": "1124.120937",
	"baseVol": "491082.129100",
	"quoteVol": "436.858805",
	"timestamp": 1588024908,
	"type": "buy"
}
```

### HTTP Запрос

`GET https://example.com/api/v1/market/trades?pairName=BTC/USDT&type=buy`

### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | наименование криптовалютной пары (В формате BTC/USDT)
type | string | Нет | Принимает значения buy или sell, если параметр не передается передаем и то и другое

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
tradeId | Integer | Да | Уникальный идентификатор сделки
price | string | Да | Цена сделки
baseVol | string | Да | Количество базовой криптовалюты, задействованное в сделке
quoteVol | string | Да | Количество котируемой криптовалюты, задействованное в сделке
timestamp | timestamp | Да | время совершения сделки в мс
type | string | Да | Тип сделки покупка/продажа. <br/>Покупка говорит о том, что после выполнения сделки в стакане убралась позиция на аск. <br/>Продажа- убралась из стакана позиция на бид.

## Orderbook

Запрос актуальных биржевых ордеров по валютной паре, может предоставлять как агрегированные, так и неагрегированные данные.

```shell
curl "http://example.com/api/v1/market/orderbook/pairName=BTC/USDT?depth=20"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"timestamp": 1588024908,
	"bids": [
		{
			"amount": "1001.2913",
			"price": "1494.9292"
		}
	],
	"asks": [
		{
			"amount": "10421.1234",
			"price": "1231.9571"
		}
	]
}
```

### HTTP Запрос

`GET https://example.com/api/v1/market/orderbook/pairName=BTC/USDT?depth=20`

### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | Наименование криптовалютной пары, например KICK/BTC
depth | int? | Нет | Глубина стакана <br/>0 или параметр не передан – полный стакан </br>5/10/20/50/100/500 количество позиций спроса и предложения, которые нужно передать (по 5, по 10 и т.д.)
level | int | Нет | 1- Лучшее предложение на покупку и лучшее предложение на продажу <br/>2- Весь стакан, отсортированный по лучшим бидам и аскам <br/>3- Весь стакан не отсортированный по лучшим бидам и аскам

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
timestamp | timestamp | Yes | Секунды с 1 января 1970 года судя по примеру, но в описании указаны миллисекунды **???**
bids | Array of string | Yes | Содержит в себе цену и количество крпитовалюты
asks | Array of string | Yes | Содержит в себе цену и количество криптовалюты

## Candles

```shell
curl "http://example.com/api/v1/market/bars/?period=5min&pairName=BTC/USDT&startTime=22814882323&endTIme32222869898"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"code": 200,
	"message": "success",
	"timestamp": 1588024908,
	"openPrice": "8392.2930",
	"closePrice": "8832.1241",
	"highPrice": "9123.2120",
	"lowPrice": "8392.2930",
	"transactionVolume": "63829012.0012",
	"transactionAmount": "271"
}
```

### HTTP Запрос

В случае, если время не указано, возвращается не более **???** результатов.

`GET https://example.com/api/v1/market/bars/?period=5min&pairName=BTC/USDT&startTime=22814882323&endTIme32222869898`

### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | Наименование криптовалютной пары, например KICK/BTC
period | string | Да | 1/3/10/60 (minutes) 1D 1M 3M
startTIme | timestamp | Нет | время начала в мс
endTime | timestamp | Нет | время окончания в мс

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
code | integer | Да | код ответа 200-,если ок
message | string | Да | текст success/error
timestamp | timestamp | Да | начальное время формирования свечи
openPrice | string | Да | цена в момент открытия свечи
closePrice | string | Да | цена в момент закрытия свечи
highPrice | string | Да | наивысшая цена в свече
lowPrice | string | Да | наименьшая цена в свече
transactionVolume | string | Да | объем транзакций в свече
transactionAmount | string | Да | количество транзакций в свече

## Status

```shell
curl "http://example.com/api/v1/status"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"code": 200,
	"status": "open",
	"message": ""
}
```

### HTTP Запрос

В случае, если время не указано, возвращается не более **???** результатов.

`GET https://example.com/api/v1/status`


### Параметры URL 

*Отсутствуют.*


### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
code | integer | Да | код 200-ОК
status | string | Да | open/close
message | string | Да | текст пояснения

## Server time

```shell
curl "http://example.com/api/v1/serverTime"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"code": 200,
	"message": "success",
	"time": 1588024908
}
```


### HTTP Запрос

В случае, если время не указано, возвращается не более **???** результатов.

`GET https://example.com/api/v1/serverTime`


### Параметры URL 

*Отсутствуют.*

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
code | integer | Да | код ответа 200-ок
message | string | Да | success/error
time | timestamp | Да | текущее серверное время в мс


# Trade 

Набор методов для выставления ордеров и получения информации об ордерах.

<aside class="warning">
Для использования данных методов требуется авторизация.
</aside>

## Cancel Order 

Метод отмены ордера.

```shell
curl "http://example.com/api/v1/orders/{orderId}"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"cancelledOrderId": "111111111",
	"comment": ""
}
```

### HTTP Запрос

В случае, если время не указано, возвращается не более **???** результатов.

`DELETE https://example.com/api/v1/orders/{orderId}`


### Параметры URL 

*Отсутствуют.*

### Параметры ответа


Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
cancelledOrderId | string | Да | уникальный идентификатор ордера
comment | string | Нет | ордер отменен / причина ошибки отмены


## Cancel All Orders 

Метод отмены группы ордеров или всех открытых ордеров.

```shell
curl "http://example.com/api/v1/orders?pairName=BTC/USDT&orderType=STOP"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"cancelledOrders": [
		{
			"cancelledOrderId": "111111",
			"comment": ""
		},
		{
			"cancelledOrderId": "222222",
			"comment": ""
		}
	]
}
```

### HTTP Запрос

`DELETE https://example.com/api/v1/orders?pairName=BTC/USDT&orderType=STOP`

### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Нет | Наименование криптовалютной пары в формате KICK/ETH
orderType | string | Нет | тип отмены stop/limit/all, если параметр не задан, по умолчанию работает all

### Параметры ответа

**???** Возможно, здесь должен быть массив значений - в случае отмены несколькхи ордеров.

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
cancelledOrderId | string | Да | уникальный идентификатор ордера
comment | string | Нет | ордер отменен / причина ошибки отмены


## Trade History 

Метод получения информации об истории сделок пользователя.

```shell
curl "http://example.com/api/v1/tradesHistory?pairName=KICK/BTC&startTime=123213123213213&endTime=32434523523535"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"trades": [
		{
			"pairName": "BTC/USDT",
			"timestamp": 1588024908,
			"side": 0,
			"price": "732.9532",
			"feeQuoted": "3.1274",
			"feeExternal": "",
			"externalFeeCurrency": "KICK",
			"buyVolume": "14523",
			"sellVolume": "823491"
		},
		{
			"pairName": "BTC/USDT",
			"timestamp": 1588024908,
			"side": 0,
			"price": "732.9532",
			"feeQuoted": "3.1274",
			"feeExternal": "",
			"externalFeeCurrency": "KICK",
			"buyVolume": "14523",
			"sellVolume": "823491"
		}
	]
}
```

### HTTP Запрос

`GET https://example.com/api/v1/tradesHistory?pairName=KICK/BTC&startTime=123213123213213&endTime=32434523523535`


### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | Наименование криптовалютной пары, например KICK/BTC
startTime | timestamp | Нет | Время начала периода, в мс
endTime | timestamp | Нет | время окончания периода, в мс


### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | Наименование крпитовалютнйо пары в формате KICK/ETH
timestamp | timestamp | Да | Время сделки,в мс
side | integer | Да | Стороны ордера <br/>0-BUY </br>1- SALE
price | string | Да | цена за единицу криптовалюты в сделке, выраженная в котируемой криптовалюте
feeQuoted | string | Да | размер комиссии в котируемой криптовалюте
feeExternal | string | Нет | размер комисиии в дополнительнйо криптовалюте
externalFeeCurrency | string | Нет | наименование криптовалюты, в которой взяли дополнительную комиссию
buyVolume | string | Да | купленный объем в сделке
sellVolume | string | Да | проданный объем в сделке


## Active Orders List

Метод получения информации об активных ордерах.

```shell
curl "http://example.com/api/v1/activeOrders?pairName=KICK/BTC"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"orders": [
		{
			"pairName": "BTC/USDT",
			"createdTimeStamp": 1588024908,
			"side": 1,
			"limitPrice": "91.9012",
			"totalBuyVolume": "124124",
			"totalSellVolume": "3243",
			"orderedAmount": "150000",
			"tpActivateLeve": "90.0000",
			"tpLimitPrice": "92.0000",
			"slLimitPrice": "85.0000",
			"tpSubmitLevel": "89.0000",
			"slSubmitLevel": "86.0000",
			"activated": 1588022908
		},
		{
			"pairName": "BTC/USDT",
			"createdTimeStamp": 1588024908,
			"side": 1,
			"limitPrice": "91.9012",
			"totalBuyVolume": "124124",
			"totalSellVolume": "3243",
			"orderedAmount": "150000",
			"tpActivateLeve": "90.0000",
			"tpLimitPrice": "92.0000",
			"slLimitPrice": "85.0000",
			"tpSubmitLevel": "89.0000",
			"slSubmitLevel": "86.0000",
			"activated": 1588022908
		}
	]
}
```

### HTTP Запрос

`GET https://example.com/api/v1/activeOrders?pairName=KICK/BTC`


### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Нет | Наименование криптовалютной пары, например KICK/BTC


### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | Наименование крпитовалютнйо пары в формате KICK/ETH
createdTimeStamp | timestamp | Да | Время создания ордера, в мс
side | integer | Да | Стороны ордера <br/>0-BUY </br>1- SALE
limitPrice | string | Нет | Возвращает значение, если при установке ордера была указана лимит цена в том случае если ордер не парный
totalBuyVolume | string | Да | итоговый купленный объем
totalSellVolume | string | Да | итоговый проданный объем
orderedAmount | string | Да | Заказанное количество криптовалюты для покупки/продажи
tpActivateLeve | string | Нет | уровень активации, параметр передается в случае, если был задан при установке ордера
tpLimitPrice | string | Нет | лимит цена блок тэйк профит, параметр передается в случае, если был задан при установке ордера
slLimitPrice | string | Нет | лимит цена блока стоп лос, параметр передается в случае, если был задан при установке ордера
tpSubmitLevel | string | Нет | стоп уровень блока тэйк профит, параметр передается в случае, если был задан при установке ордера
slSubmitLevel | string | Нет | стоп уровень блока стоп лосс, параметр передается в случае, если был задан при установке ордера
activated | timestamp | Нет | время (в мс) передается если ордер активировался (если был выставлен скользящий или скользящий +сл ордер)


## Create Trade Order 

установка ордера

```shell
curl "http://example.com/api/v1/orders/createTradeOrder"
  -X POST
  -H "Authorization: meowmeowmeow"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"orderId": 123456
}
```

### HTTP Запрос

`POST https://example.com/api/v1/orders/createTradeOrder`


### Параметры запроса 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | Наименование крпитовалютнйо пары (*пример: KICK/ETH*)
orderedAmount | string | Да | Заказанное количество криптовалюты для покупки/продажи
limitPrice | string | Нет | **???** Возвращает значение, если при установке ордера была указана лимит цена в том случае если ордер не парный
tradeIntent | integer | Да | сейчас принимает значения 0 -покупка базовой и 1 - продажа базовой криптовалюты
modifier | integer | Нет | сейчас принимает только значение GTC, если параметр не указан выставляется он же
reserves | integer | Нет | 0 (по умолчанию) резервы не делать, 1 - резервы делать. работает только в случае если указана лимит цена


### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
orderId | integer | Да | Идентификатор созданного ордера


## Create Stop Order 

установка ордера

```shell
curl "http://example.com/api/v1/orders/createStopOrder"
  -X POST
  -H "Authorization: meowmeowmeow"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"orderId": 123456
}
```

### HTTP Запрос

`POST https://example.com/api/v1/orders/createStopOrder`


### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
pairName | string | Да | Наименование крпитовалютнйо пары в формате KICK/ETH
orderedAmount | string | Да | Заказанное количество криптовалюты для покупки/продажи
tradeIntent | integer | Да | сейчас принимает значения 0 -покупка базовой и 1 - продажа базовой криптовалюты
modifier | integer | Нет | сейчас принимает только значение GTC, если параметр не указан выставляется он же
reserves | integer | Нет | 0 (по умолчанию) резервы не делать, 1 - резервы делать. работает только в случае если указана лимит цена
tpActivateLevel | string | Нет | уровень активации,
tpLimitPrice | string | Нет | лимит цена блок тэйк профит,
slLimitPrice | string | Нет | лимит цена блока стоп лос
tpSubmitLevel | string | Нет | стоп уровень блока тэйк профит
slSubmitLevel | string | Нет | стоп уровень блока стоп лосс

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
orderId | integer | Да | Идентификатор созданного ордера

# User 

Набор методов для получения информации о пользователе и его аккаунте на бирже 

<aside class="warning">
Для использования данных методов требуется авторизация.
</aside>

## User Info 

Основные данные о пользователе.

```shell
curl "http://example.com/api/v1/userInfo"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"userId": 111111111,
	"userName": "kickuser123",
	"platformName": "KickEX",
	"comment": "",
	"restrictions": 0
}
```

### HTTP Запрос

`GET https://example.com/api/v1/userInfo`

### Параметры URL 

*Отсутствуют.*

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
userId | integer | Да | идентификатор Пользователя
userName | string | Нет | слаг Пользователя
platformName | string | Да | KickEX
comment | string | Нет | Комментарий, может содержать информацию, касательно ограничений на действия с АПИ Пользоватем
restrictions | integer | Да | Индикатор, показывающий, доступна ли торговля Пользователю (0 – доступна) 1 – не доступна

## Balance

Информация о балансе пользователя;

```shell
curl "http://example.com/api/v1/user/balance"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"balances": [
		{
			"currencyName": "KICK",
			"balance": "10000000.8372",
			"available": "598292.1214",
			"inOrders": "300123.9133",
			"accountType": "2401"
		},
		{
			"currencyName": "ETH",
			"balance": "10000000.8372",
			"available": "598292.1214",
			"inOrders": "300123.9133",
			"accountType": "2401"
		}
	]
}
```

### HTTP Запрос

`GET https://example.com/api/v1/user/balance`

### Параметры URL 

*Отсутствуют.*

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
currencyName | string | Да | наименование криптовалюты краткое
balance | string | Да | количество средств (тотал)
available | string | Да | количество средств, доступных для вывода или торговли
inOrders | string | Да | количество зарезервированных средств
accountType | string | Да | номер счета <br/>2401 - основной счет <br/>2411 - экосистемный счет в валюте брокера

## Deposit Address 

Метод получения персонального адреса для пополнения.

```shell
curl "http://example.com/api/v1/depositAddresses?currencyName=USDT&chain=ERC20"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"currencyName": "USDT",
	"chain": "ERC20",
	"memo": "123456",
	"address": "0xc0DAa9e14343128cd50f7b934B5Bb23eddd3F246"
}
```

### HTTP Запрос

`GET https://example.com/api/v1/depositAddresses?currencyName=USDT&chain=ERC20`

### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
currencyName | string | Да | Наименование криптовалюты
chain | string | Нет | ERC20/OMNI/TRC20 какой выберем по дефолту для USDT?

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
currencyName | string | Да | Наименование криптовалюты
chain | string | Нет | ERC20/OMNI/TRC20
memo | string | Нет | необходим для xrp валют? в остальных случаях не нужен?
address | string | Да | адрес для пополнения


## Deposit History 

Метод получения истории пополнений.

```shell
curl "http://example.com/api/v1/depositHistory?сurrencyName=KICK&startTime=1588015708&endTime=1588024908&status=success"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"deposits": [
		{
			"address": "0xc0DAa9e14343128cd50f7b934B5Bb23eddd3F246",
			"amount": "200000.0000",
			"fee": "",
			"currencyName": "KICK",
			"memo": "",
			"walletTxId": "",
			"status": "success",
			"createdAt": 1588024908,
			"updatedAt": 1588024908,
			"comment": ""
		},
		{
			"address": "0xc0DAa9e14343128cd50f7b934B5Bb23eddd3F246",
			"amount": "200000.0000",
			"fee": "",
			"currencyName": "KICK",
			"memo": "",
			"walletTxId": "0x3f9a6dc91d0ac08e2d13fc3a42a9dc4481aade8a96e10c1f497f9d6c60130a15",
			"status": "success",
			"createdAt": 1588024908,
			"updatedAt": 1588024908,
			"comment": ""
		}
	]
}
```

### HTTP Запрос

`GET https://example.com/api/v1/depositHistory?сurrencyName=KICK&startTime=1588015708&endTime=1588024908&status=success`

### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
сurrencyName | string | Нет | наименование криптовалюты, краткое, например BTC
startTime | timestamp | Нет | Время начала периода, в мс
endTime | timestamp | Нет | время окончания периода, в мс
status | string | Нет | фильтр статусов депозита (failure/success/processing)

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
address | string | Да | адрес, на который было произведено пополнение
amount | string | Да | количество пополненной криптовалюты
fee | string | Да | комиссия за пополнение
currencyName | string | Да | наименование криптовалюты (краткое), например, BTC
memo | string | Нет | мемо метка (если есть, отображаем)
walletTxId | string | Да | хэш транзакции
status | string | Да | failure/success/processing
createdAt | timestamp | Да | время создания записи в бд
updatedAt | timestamp | Да | время обновления записи в бд
comment | string | Нет | комментарий (при наличии)

## Withdraw 

Метод создания запроса на вывод средств.

```shell
curl "http://example.com/api/v1/user/withdraw"
  -X POST
  -H "Authorization: meowmeowmeow"
  -H "Content-Type: application/json"
  -d '{"address":"0xc0DAa9e14343128cd50f7b934B5Bb23eddd3F246",
	   "memo":"",
	   "amount":"1000",
	   "currency":"KICK",
	   "chain":"ERC20"}'  
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"orderId": 123456
}
```

### HTTP Запрос

`POST https://example.com/api/v1/user/withdraw`


### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
address | string | Да | адрес, на который выводятся средства
memo | string | Нет | мемо тег (опционально)
amount | string | Да | количество криптовалюты для вывода
currency | string | Да | криптовалюта, в которой осуществляется вывод
сhain | string | Нет | Если чейнов несколько, как с USDT, то отображается чейн на который был вывод

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
orderId | integer | Да | Идентификатор созданного ордера

## Withdrawal History 

Метод для запроса истории вывода средств.

```shell
curl "http://example.com/api/v1/withdrawalHistory?сurrencyName=KICK&startTime=1588015708&endTime=1588024908&status=success"
```

> Команда выше вернёт структуру следующего вида:

```json
{
	"withdrawals": [
		{
			"transactionId": "123415",
			"address": "0xc0DAa9e14343128cd50f7b934B5Bb23eddd3F246",
			"amount": "200000.0000",
			"fee": "",
			"currencyName": "KICK",
			"memo": "",
			"walletTxId": "",
			"status": "processing",
			"createdAt": 1588024908,
			"updatedAt": 1588024908,
			"comment": ""
		},
		{
			"transactionId": "123416",
			"address": "0xc0DAa9e14343128cd50f7b934B5Bb23eddd3F246",
			"amount": "200000.0000",
			"fee": "",
			"currencyName": "KICK",
			"memo": "",
			"walletTxId": "0x3f9a6dc91d0ac08e2d13fc3a42a9dc4481aade8a96e10c1f497f9d6c60130a15",
			"status": "success",
			"createdAt": 1588024908,
			"updatedAt": 1588024908,
			"comment": ""
		}
	]
}
```

### HTTP Запрос

`GET https://example.com/api/v1/withdrawalHistory?сurrencyName=KICK&startTime=1588015708&endTime=1588024908&status=success`

### Параметры URL 

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
сurrencyName | string | Нет | наименование криптовалюты, краткое, например BTC
startTime | timestamp | Нет | Время начала периода, в мс
endTime | timestamp | Нет | время окончания периода, в мс
status | string | Нет | failure/success/processing/wallet_processing

### Параметры ответа

Параметр | Тип | Обязательный | Описание
--------- | ----------- | ----------- | -----------
transactionId | string | Да | Уникальный идентификатор транзакции
address | string | Да | адрес, на который был произведен вывод
amount | string | Да | количество отправленной криптовалюты
fee | string | Да | комиссия за вывод
currencyName | string | Да | наименование криптовалюты (краткое), например, BTC
memo | string | Нет | мемо метка (если есть, отображаем)
walletTxId | string | Да | хэш транзакции
status | string | Да | failure/success/processing
createdAt | timestamp | Да | время создания записи в бд
updatedAt | timestamp | Да | время обновления записи в бд
comment | string | Нет | комментарий (при наличии)
chain | string | Нет | Если чейнов несколько, как с USDT, то отображается чейн на который был вывод