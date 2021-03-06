# upbit-api
[![npm](https://img.shields.io/npm/v/upbit-api.svg?style=flat-square)](https://www.npmjs.com/package/upbit-api)
[![npm](https://img.shields.io/npm/dt/upbit-api.svg?style=flat-square)](https://www.npmjs.com/package/upbit-api)
[![npm](https://img.shields.io/npm/l/upbit-api.svg?registry_uri=https%3A%2F%2Fregistry.npmjs.com&style=flat-square)](https://opensource.org/licenses/MIT)
[![npm](https://img.shields.io/badge/Readme-English-lightgray.svg?style=flat-square)](https://github.com/Shin-JaeHeon/upbit-api/blob/master/README.md)
[![npm](https://img.shields.io/badge/Readme-한국어-blue.svg?style=flat-square)](https://github.com/Shin-JaeHeon/upbit-api/blob/master/README-KR.md)
[![npm](https://img.shields.io/badge/Readme-日本語-orange.svg?style=flat-square)](https://github.com/Shin-JaeHeon/upbit-api/blob/master/README-JP.md)
[![npm](https://img.shields.io/badge/Readme-汉语-orange.svg?style=flat-square)](https://github.com/Shin-JaeHeon/upbit-api/blob/master/README-CN.md)

upbit-apiはUpbitのOpen APIをより容易に使用できるように作ったnode.js用ライブラリです。

タイプスクリプトで作成されており、es2017にコンパイルされています。

Restful APIとWebSocket APIを支援するのが目標です。

## ticker(market)
`Market`の(KRW-BTCのようなものを指します。)配列を生成します。

  | パラメータ       | タイプ                       | 説明                                 |
|----------------|--------------------------- |-------------------------------------|
| market         | string または Array\<string\>  | 'KRW-BTC' または ['KRW-BTC', 'KRW-XRP'] |
### Market class
| 名                | タイプ | 説明                                 |
|-------------------|--------|--------------------------------------|
| market            | string | 例) KRW, BTC, USDT ...               |
| coin              | string | 例) BTC, ETH, XRP ...                |
| marketCode        | string | 例) KRW-BTC, KRW-XRP ...             |
| tradeTime         | `Date` | 取引時間                             |
| price             | number | 価格                                 |
| open              | number | 時価                                 |
| high              | number | 高価                                 |
| low               | number | 最低価格                             |
| prevClose         | number | 前日終値                             |
| change            | number | EVEN(横ばい), RISE(上昇), FALL(下落) |
| changePrice       | number | 変化金額の絶対値                     |
| changeRate        | number | 変化率の絶対値                       |
| signedChangePrice | number | 符号がある変化の金額                 |
| signedChangeRate  | number | 符号がある変化率                     |
| tradeVolume       | number | 最新の取引量                         |
| accTradePrice     | number | 累積取引代金(UTC 0時基準)            |
| accTradePrice24   | number | 24時間の累積取引代金                 |
| accTradeVolume    | number | 累積取引量(UTC 0時基準)              |
| accTradeVolume24  | number | 24時間の累積取引代金                 |
| high52wPrice      | number | 52週の新しい高価                     |
| high52wDate       | `Date` | 52注意新しい高価達成日               |
| low52wPrice       | number | 52注意新しい最低価格                 |
| low52wDate        | `Date` | 52注意新しい最低価格達成日           |
| lastUpdate        | `Date` | このオブジェクトが更新された時刻     |
## autoMarketUpdate(market, time , errorHandler, callback?)
`Market`のオブジェクトを一定時間ごとにアップデートします。

| パラメータ   | タイプ                          | 説明                                                   |
|--------------|---------------------------------|--------------------------------------------------------|
| market       | `Market` または Array\<Market\> | アップデートなる  `Market` オブジェクト                |
| time         | number                          | アップデート周期 (ミリ秒)                              |
| errorHandler | function, (error) => any        | エラーハンドラ                                         |
| callback     | function, (market) => any       | 選択事項、オブジェクトが更新されときに呼び出されます。 |

## OrderBook(market)
`OrderBook`の配列を生成します。

| パラメータ       | タイプ                       | 説明                                 |
|----------------|--------------------------- |-------------------------------------|
| market         | string または Array\<string\>  | 'KRW-BTC' または ['KRW-BTC', 'KRW-XRP'] |

### OrderBook クラス
| 名         | タイプ           | 説明                             |
|------------|------------------|----------------------------------|
| market     | string           | 例) KRW, BTC, USDT ...           |
| coin       | string           | 例) BTC, ETH, XRP ...            |
| marketCode | string           | 例) KRW-BTC, KRW-XRP ...         |
| lastUpdate | `Date`           | このオブジェクトが更新された時刻  |
| askList    | Array\<`Order`\> | Ask オーダーリスト               |
| bidList    | Array\<`Order`\> | Bid オーダーリスト               |
| totalAsk   | number           | total ask                        |
| totalBid   | number           | total bid                        |

### Order クラス
| 名    | タイプ | 説明   |
|-------|--------|--------|
| price | number | 価格   |
| size  | number | 注文量 |

## autoOrderBookUpdate(orderBook, time , errorHandler, callback?)
`OrderBook`のオブジェクトを一定時間ごとにアップデートします。

| パラメータ       | タイプ                         | 説明                                   |
|----------------|---------------------------   |---------------------------------------|
| orderBook         | `OrderBook` または Array\<OrderBook\>  |アップデートなる  `OrderBook` オブジェクト |
| time           | number                       | アップデート周期 (ミリ秒) |
| errorHandler   | function, (error) => any     | エラーハンドラ  |
| callback   | function, (orderBook) => any     |  選択事項、オブジェクトが更新されときに呼び出されます。 |

## ticks(market)
`Trade`の配列を生成します。

| パラメータ     | タイプ                      | 説明                                |
|----------------|--------------------------- |-------------------------------------|
| params         | string または Array\<string\>  | 'KRW-BTC' or ['KRW-BTC', 'KRW-XRP'] |
| count          | number                     | count                               |
| to             | string                     | HHmmss or HH:mm:ss                  |
| cursor         | number                     | sequential_id                       |

### Trade クラス
| 名     | タイプ   | 説明      |
|--------------------|-------  |-------------|
| market             | string  | 例) KRW, BTC, USDT ... |
| coin               | string  | 例) BTC, ETH, XRP ... |
| marketCode         | string  | 例) KRW-BTC, KRW-XRP ... |
| lastUpdate         | `Date`  | このオブジェクトが更新された時刻|
| tradeTime          | `Date`  | 締結時間 |
| price              | number  | 締結の価格 |
| volume             | number  | 締結取引量  |
| prev_closing_price | number  | 前日終値 |
| change_price       | number  | 変化量  |
| isAsk              | boolean | 罵倒/買収 |
| sequential_id      | number  | 締結番号(Unique)  |

## candlesMinutes(market, unit?, count?, to?)
`Candle`の配列を生成します。

| パラメータ     | タイプ                      | 説明                                |
|----------------|--------------------------- |-------------------------------------|
| market         | string or Array\<string\>  | 'KRW-BTC' or ['KRW-BTC', 'KRW-XRP'] |
| unit           | number                     |  1, 3, 5, 15, 10, 30, 60, 240       |
| count          | number                     | count                               |
| to             | string                     | yyyy-MM-dd'T'HH:mm:ssXXX            |

### Candle クラス
| 名                | タイプ | 説明                                                      |
|-------------------|--------|-----------------------------------------------------------|
| market            | string | 例) KRW, BTC, USDT ...                                    |
| coin              | string | 例) BTC, ETH, XRP ...                                     |
| marketCode        | string | 例) KRW-BTC, KRW-XRP ...                                  |
| timestamp         | number | 最後のtickがキャンドルに保存された時間                      |
| candleDateTimeUTC | `Date` | Standard time of the candle (UTC basis)                   |
| candleDateTimeKST | `Date` | Standard time of the candle (KST basis)                   |
| open              | number | Market value                                              |
| high              | number | 高価                                                      |
| low               | number | 最低価格                                                   |
| accTradePrice     | number | Candle's accTradePrice                                    |
| accTradeVolume    | number | Candle's cumulative transaction amount                    |
| lastUpdate        | `Date` | このオブジェクトが更新された時刻ed                         |
#### MinutesCandle クラス
`MinutesCandle` extends `Candle`

| 名   | タイプ | 説明                                                   |
|------|--------|--------------------------------------------------------|
| unit | number |分です、 使用可能な値: 1, 3, 5, 15, 10, 30, 60, 240 |
#### DayCandle クラス
`DayCandle` extends `Candle`

| 名                  | タイプ | 説明                                  |
|---------------------|--------|---------------------------------------|
| prevClosingPrice    | number | 前日終値 |
| convertedTradePrice | number | 指定した貨幣に換算した価格             |
| changePrice         | number | 変化金額                              |
| changeRate          | number | 変化率                                |
#### WeekMonthCandle クラス
`WeekMonthCandle` extends `Candle`

| 名               | タイプ | 説明   |
|------------------|--------|--------|
| firstDayOfPeriod | number | 期首日 |
## allMarket()
Upbitで取引できるマーケットのリスト.

パラメータはありせん。
| 名           | タイプ | 説明                                 |
|--------------|--------|--------------------------------------|
| market       | string | Upbitのマーケットの情報, 例) BTC-XRP |
| korean_name  | string | 韓国語名 例) 비트코인                |
| english_name | string | 英語名 例) Bitcoin                 |

翻訳に間違いがあれば、PRお願いします。
