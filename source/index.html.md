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

Kittn requires an API key to be included in all API requests to the server in a header that looks like the following:

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
	"price": "1124.120937",
	"baseVol": "491082.129100",
	"quoteVol": "436.858805",
	"timestamp": 1588024908,
	"type": "buy"
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


## Candles

```shell
curl "http://example.com/api/v1/market/bars/?period=5min&pairName=BTC/USDT&startTime=22814882323&endTIme32222869898"
```

> The above command returns JSON structured like this:

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
	"code": 200,
	"status": "open",
	"message": ""
}
```

### HTTP Request

If time is not specified, **???** results is returned.

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
	"code": 200,
	"message": "success",
	"time": 1588024908
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

```shell
curl "http://example.com/api/v1/orders/{orderId}"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
	"cancelledOrderId": "111111111",
	"comment": ""
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


```shell
curl "http://example.com/api/v1/orders?pairName=BTC/USDT&orderType=STOP"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

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


## Trade History 

This method is used to get data on the user's trades.

```shell
curl "http://example.com/api/v1/tradesHistory?pairName=KICK/BTC&startTime=123213123213213&endTime=32434523523535"
```

> The above command returns JSON structured like this:

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

### HTTP Request

`GET https://example.com/api/v1/tradesHistory?pairName=KICK/BTC&startTime=123213123213213&endTime=32434523523535`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string | Yes | Currency pair name *(ex: KICK/BTC)*
startTIme | timestamp |  | Start time in milliseconds
endTime | timestamp |  | End time in milliseconds


### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string | Yes | Currency pair name *(ex: KICK/ETH)*
timestamp | timestamp | Yes | Trade timestamp
side | integer | Yes | Trade side <br/> 0 - BUY <br/>1 - SALE
price | string | Yes | Price per currency unit (in quotes currency)
feeQuoted | string | Yes | Fee (in quoted currency)
feeExternal | string | No | Fee (in additional currency)
externalFeeCurrency | string | No | Additional fee currency
buyVolume | string | Yes | Trade buy volume
sellVolume | string | Yes | Trade sell volume


## Active Orders List

Method used to get information regarding all user's open (active) exchange orders.

```shell
curl "http://example.com/api/v1/activeOrders?pairName=KICK/BTC"
```

> The above command returns JSON structured like this:

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

### HTTP Request

`GET https://example.com/api/v1/activeOrders?pairName=KICK/BTC`

### URL Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string | No | Currency pair name *(ex: KICK/BTC)*


### Response Parameters
Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string | Yes | Currency pair name *(ex: KICK/ETH)*
createdTimeStamp | timestamp | Yes | Order creation timestamp
side | integer | Yes | Trade side <br/> 0 - BUY <br/>1 - SALE
limitPrice | string | No | Will be returned for orders where limit price was set on creation.
totalBuyVolume | string | Yes | Total bought volume **???**
totalSellVolume | string | Yes | Total sold volume **???**
orderedAmount | string | Yes | Ordered amount of currency
tpActivateLeve | string | No | Take profit activation level, will be returned if set on order creation.
tpLimitPrice | string | No | Take profit limit price, will be returned if it was set on order creation.
slLimitPrice | string | No | Stop loss limit price, will be returned if it was set on order creation.
tpSubmitLevel | string | No | Take profit stop level, will be returned if it was set on order creation.
slSubmitLevel | string | No | Stop loss stop level, will be returned if it was set on order creation.
activated | timestamp | No | Will be returned if the order was activated (for sliding orders) **???**

## Create Trade Order 

Method for trade order creation.

```shell
curl "http://example.com/api/v1/orders/createTradeOrder"
  -X POST
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
	"orderId": 123456
}
```

### HTTP Request

`POST https://example.com/api/v1/orders/createTradeOrder`

### Request Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string | Yes | Currency pair name *(ex: KICK/ETH)*
orderedAmount | string | Yes | Ordered currency amount
limitPrice | string | No | **???**
tradeIntent | integer | Yes | Possible values:<br/>0 - buy base currency, <br/>1 - sell base currency
modifier | integer | No | Possible value: GTC (if ommitted, the same is used)
reserves | integer | No | 0 (default) - don't create reserves, <br/>1 - create reserves (valid only if limitPrice is set)


### Response Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
orderId | integer | Yes | Created trade order identifier

## Create Stop Order 

Method for stop order creation.

```shell
curl "http://example.com/api/v1/orders/createStopOrder"
  -X POST
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
	"orderId": 123456
}
```

### HTTP Request

`POST https://example.com/api/v1/orders/createStopOrder`

### Request Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
pairName | string | Yes | Currency pair name *(ex: KICK/ETH)*
orderedAmount | string | Yes | Ordered currency amount
tradeIntent | integer | Yes | Currently two possible values are accepted: <br/>0 - buying base currency <br/>1 - selling base currency
modifier | integer | No | Possible value: GTC (if ommitted, the same is used)
reserves | integer | No | 0 (default) - don't create reserves, <br/>1 - create reserves (valid only if limitPrice is set)
tpActivateLevel | string | No | Take profit activation level
tpLimitPrice | string | No | Take profit stop level
slLimitPrice | string | No | Stop loss limit price
tpSubmitLevel | string | No | Take profit submit level
slSubmitLevel | string | No | Stop loss submit level

### Response Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
orderId | integer | Yes | Created trade order identifier

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
	"userName": "kickuser123",
	"platformName": "KickEX",
	"comment": "",
	"restrictions": 0
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
curl "http://example.com/api/v1/depositAddresses?currencyName=USDT&chain=ERC20"
```

> The above command returns JSON structured like this:

```json
{
	"currencyName": "USDT",
	"chain": "ERC20",
	"memo": "123456",
	"address": "0xc0DAa9e14343128cd50f7b934B5Bb23eddd3F246"
}
```

### HTTP Request

`GET https://example.com/api/v1/depositAddresses?currencyName=USDT&chain=ERC20`

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
curl "http://example.com/api/v1/depositHistory?сurrencyName=KICK&startTime=1588015708&endTime=1588024908&status=success"
```

> The above command returns JSON structured like this:

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

### HTTP Request

`GET https://example.com/api/v1/depositHistory?сurrencyName=KICK&startTime=1588015708&endTime=1588024908&status=success`

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

> The above command returns JSON structured like this:

```json
{
	"orderId": 123456
}
```

### HTTP Request


`POST https://example.com/api/v1/user/withdraw`

### Request Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
address | string | Yes | External address for withdrawal
memo | string | No | Memo tag
amount | string | Yes | Amount to withdraw
currency | string | Yes | Currency *(example: USDT)*
сhain | string | No | Blockchain (needed for currencies like USDT that are present in several blockchains)

### Response Parameters

Parameter | Type | Required | Description
--------- | ----------- | ----------- | -----------
orderId | integer | Yes | Created trade order identifier

## Withdrawal History 

Method to get withdrawal history.

```shell
curl "http://example.com/api/v1/withdrawalHistory?сurrencyName=KICK&startTime=1588015708&endTime=1588024908&status=success"
```

> The above command returns JSON structured like this:

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

### HTTP Request

`GET https://example.com/api/v1/withdrawalHistory?сurrencyName=KICK&startTime=1588015708&endTime=1588024908&status=success`

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
