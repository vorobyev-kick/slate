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

## Trades

This method returns deals history during last 24 hours.

```shell
curl "http://example.com/api/v1/market/trades?pairName=BTC/USDT&type=buy"
```

> The above command returns JSON structured like this:

```json
{
	"tradeId": 111111111,
	"price": 111111111,
	"baseVol": 111111111,
	"quoteVol": 111111111,
	"timestamp": 111111111,
	"type": 111111111
}
```

### HTTP Request

`GET https://example.com/api/v1/market/trades?pairName=BTC/USDT&type=buy`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string | Да | наименование криптовалютной пары (В формате BTC/USDT)
type | string | Нет | Принимает значения buy или sell, если параметр не передается передаем и то и другое

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
tradeId | Integer | Yes | Trade unique identifier
price | string | Yes | Trade price
baseVol | string | Yes | Base currency volume
quoteVol | string | Yes | Quotes currency volume
timestamp | timestamp | Yes | Trade timestamp
type | string | Yes | Trade type: <br/>buy - means that an ask position was removed from the exchange order book; <br/>sell - means that a bid position was removed from the exchange order book.

## Orderbook

This request is used to get current exchange orders by currency pair name.
Provides both aggregated and particular data.

```shell
curl "http://example.com/api/v1/market/orderbook/pairName=BTC/USDT?depth=20"
```

> The above command returns JSON structured like this:

```json
{
	"timestamp": 111111111,
	"bids": 111111111,
	"asks": 111111111
}
```

### HTTP Request

`GET https://example.com/api/v1/market/orderbook/pairName=BTC/USDT?depth=20`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string | Yes | Currency pair name *(ex: KICK/BTC)*
depth | int? | No | Orderbook depth.<br/>0 or null - all available data <br/>5/10/20/50/100/500 - number of bid and ask positions to show
level | int | No | 1 - Best buy and sell open trades <br>2 - Whole orderbook sorted by best bid and ask prices <br> 3 - Whole orderbook (not sorted)

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
timestamp | timestamp | Yes | Timestamp
bids | Array of string | Yes | List of bids (price and amount)
asks | Array of string | Yes | List of asks (price and amount)

## Trade history

???

## Candles

```shell
curl "http://example.com/api/v1/market/bars/?period=5min&pairName=BTC/USDT&startTime=22814882323&endTIme32222869898"
```

> The above command returns JSON structured like this:

```json
{
	"code": 111111111,
	"message": 111111111,
	"timestamp": 111111111,
	"openPrice": 111111111,
	"closePrice": 111111111,
	"highPrice": 111111111,
	"lowPrice": 111111111,
	"transactionVolume": 111111111,
	"transactionAmount": 111111111
}
```

### HTTP Request

If `startTime` or `endTime` are not provided, not more than **???** results are returned.

`GET https://example.com/api/v1/market/bars/?period=5min&pairName=BTC/USDT&startTime=22814882323&endTIme32222869898`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string |  | Currency pair name *(ex: KICK/BTC)*
period | string |  | 1/3/10/60 (minutes) 1D 1M 3M
startTIme | timestamp |  | Start time in milliseconds
endTime | timestamp |  | End time in milliseconds

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
code | integer | Yes | Response code (200 for OK)
message | string | Yes | *success*/*error*
timestamp | timestamp | Yes | Timestamp of candle creation
openPrice | string | Yes | Open price of the candle
closePrice | string | Yes | Close price of the candle
highPrice | string | Yes | Highest price
lowPrice | string | Yes | Lowest price
transactionVolume | string | Yes | Trades volume within the candle
transactionAmount | string | Yes | Trades number within the candle

## Status

```shell
curl "http://example.com/api/v1/status"
```

> The above command returns JSON structured like this:

```json
{
	"code": 111111111,
	"status": 111111111,
	"message": 111111111
}
```

### HTTP Request

`GET https://example.com/api/v1/status`

### URL Parameters

*None.*

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
code | integer | Yes | Response code (200 for OK)
status | string | Yes | *open*/*close*
message | string | Yes | Text describing reasons for current status.

## Server time

```shell
curl "http://example.com/api/v1/serverTime"
```

> The above command returns JSON structured like this:

```json
{
	"code": 111111111,
	"message": 111111111,
	"time": 111111111
}
```

### HTTP Request

`GET https://example.com/api/v1/serverTime`

### URL Parameters

*None.*

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
code | integer | Yes | Response code (200 for OK)
message | string | Yes | *success*/*error*
time | timestamp | Yes | Current server time (in milliseconds)


# Trade 

This section covers methods that operate with exchange orders.

<aside class="warning">
Authorization is needed to use these methods.
</aside>

## Cancel Order 

Exchange order cancellation method.

**???**
```shell
curl "http://example.com/api/v1/status"
```

> The above command returns JSON structured like this:

```json
{
	"cancelledOrderId": 111111111,
	"comment": 111111111
}
```

### HTTP Request

`DELETE https://example.com/api/v1/orders/{orderId}`

### URL Parameters

*None.*


### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
cancelledOrderId | string | Yes | Cancelled exchange order identifier
comment | string | No | Contains result: order cancelled or error

## Cancel All Orders

Method used to cancel a group of orders or all the open orders.


**???**
```shell
curl "http://example.com/api/v1/status"
```

> The above command returns JSON structured like this:

```json
{

}
```

### HTTP Request

`DELETE https://example.com/api/v1/orders?pairName=BTC/USDT&orderType=STOP`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string | No | Currency pair name *(ex: KICK/ETH)*
orderType | string | No | Type of the orders to cancel (stop/limit/all), missing order type is treated as "all".


### Response Parameters

**???** Should here be an object array?

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
cancelledOrderId | string | Yes | Cancelled exchange order identifier
comment | string | No | Contains result: order cancelled or error

## Place Order 

установка ордера





## Active Orders List 

получение информации об активных ордерах

## Orders List 

получение информации о завершенных ордерах

## Trade List 

получение информации об истории сделок Пользователя

# User 

This section covers methods getting information regarding user and his or her account on the Exchange.

<aside class="warning">
Authorization is needed to use these methods.
</aside>


## User Info 

Main user data.

```shell
curl "http://example.com/api/v1/userInfo"
```

> The above command returns JSON structured like this:

```json
{
	"userId": 111111111,
	"userName": 111111111,
	"platformName": 111111111,
	"comment": 111111111,
	"restrictions": 111111111
}
```

### HTTP Request

`GET https://example.com/api/v1/userInfo`

### URL Parameters

*None.*

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
userId | integer | Yes | User identifier
userName | string | No | User nickname
platformName | string | Yes | KickEX
comment | string | No | Human-readable (?) comment that may contain restrictions applied to using API by the user.
restrictions | integer | Yes | Attribute showing if trading is blocked for the user (0 - available, 1 - blocked)

## Balance

User balance data.

```shell
curl "http://example.com/api/v1/user/balance"
```

> The above command returns JSON structured like this:

```json
{
	"currencyName": 111111111,
	"balance": 111111111,
	"available": 111111111,
	"inOrders": 111111111,
	"accountType": 111111111
}
```

### HTTP Request

`GET https://example.com/api/v1/user/balance`

### URL Parameters

*None.*

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
currencyName | string | Yes | Currency short name
balance | string | Yes | Total balance
available | string | Yes | Balance available for withdrawal
inOrders | string | Yes | Reserved balance
accountType | string | Yes | Account type:<br/> 2401 - ordinary account <br/> 2411 - Ecosystem account

## Deposit Address 

Method for getting personal deposit address.

```shell
curl "http://example.com/api/v1/depositAddresses"
```

> The above command returns JSON structured like this:

```json
{
	"currencyName": 111111111,
	"balance": 111111111,
	"available": 111111111,
	"inOrders": 111111111,
	"accountType": 111111111
}
```

### HTTP Request

`GET https://example.com/api/v1/depositAddresses`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
currencyName | string | Yes | Currency short name
chain | string | No | Blockchain short name: ERC20/OMNI/TRC20 (required for cryptocurrencies available in several blockchains)

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
currencyName | string | Yes | Currency short name
chain | string | No | Blockchain short name (required for cryptocurrencies available in several blockchains)
memo | string | No | Required for XRP
address | string | Yes | Address in specified blockchain

## Deposit History 

This method provides deposit history.

```shell
curl "http://example.com/api/v1/depositHistory"
```

> The above command returns JSON structured like this:

```json
{
	"currencyName": 111111111,
	"balance": 111111111,
	"available": 111111111,
	"inOrders": 111111111,
	"accountType": 111111111
}
```

### HTTP Request

`GET https://example.com/api/v1/depositHistory`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
сurrencyName | string | No | Currency short name
startTime | timestamp | No | Start time of the report
endTime | timestamp | No | End time of the report
status | string | No | Deposit status filtering (failure/success/processing)

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
address | string | Yes | Deposit address
amount | string | Yes | Deposit amount
fee | string | Yes | Deposit commission (if any)
currencyName | string | Yes | Currency short name
memo | string | No | Memo or tag (if present)
walletTxId | string | Yes | Transaction hash
status | string | Yes | Transaction status (failure/success/processing)
createdAt | timestamp | Yes | Database record creation timestamp
updatedAt | timestamp | Yes | Database record update timestamp
comment | string | No | Comment (if any)

## Withdraw 

Method for withdrawal request creation.

## Withdraw History 

Method to get withdrawal history.

```shell
curl "http://example.com/api/v1/withdrawalHistory"
```

> The above command returns JSON structured like this:

```json
{
	"transactionId": 111111111,
	"address": 111111111,
	"amount": 111111111,
	"fee": 111111111,
	"currencyName": 111111111,
	"memo": 111111111,
	"walletTxId": 111111111,
	"status": 111111111,
	"createdAt": 111111111,
	"updatedAt": 111111111,
	"comment": 111111111,
	"chain": 111111111
}
```

### HTTP Request

`GET https://example.com/api/v1/withdrawalHistory`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
сurrencyName | string | No | Currency short name
startTime | timestamp | No | Start time of the report
endTime | timestamp | No | End time of the report
status | string | No | Withdrawal status filtering (failure/success/processing/wallet_processing)

### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
transactionId | string | Yes | Unique identifier of withdrawal transaction
address | string | Yes | Withdrawal address
amount | string | Yes | Withdrawal amount
fee | string | Yes | Withdrawal commission
currencyName | string | Yes | Currency short name
memo | string | No | Memo or tag (if any)
walletTxId | string | Yes | Transaction hash
status | string | Yes | Transaction status (failure/success/processing)
createdAt | timestamp | Yes | Database record creation timestamp
updatedAt | timestamp | Yes | Database record update timestamp
comment | string | No | Comment (if any)
chain | string | No | Blockchain short name (required for cryptocurrencies available in several blockchains)

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

