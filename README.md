# moneywagonjs
Multi-blockchain service API client library for javascript

This library is a direct port of the python library of the same name.

## Usage

Call to the getCurrentPrice function will make an ajax call to some blockchain
service API, the result is passed onto the callback function.

```js
moneywagon.getCurrentPrice('btc', 'usd', function(price, source) {
    console.log(price, source);
});
```

    [391.324, 'bitstamp']

The first argument is the crypto price, the second argument is the fiat price.
`source` is the string of the service used, `price` is the conversion ratio.

```js
moneywagon.getCurrentPrice('ltc', 'rur', function(price, source) {
    console.log(price, "litecoins equals 1 russian ruble, according to", source);
});
```

    169.54116322 litecoins equals 1 russian ruble, according to cryptonator

Custom service fallback order:

```js
var service = new moneywagon.CurrentPrice([
    moneywagon.BTCE,
    moneywagon.Bitstamp
]);

console.log(service.get('btc', 'usd'));
```

    [377.2, 'btce']

```js
var service = new moneywagon.CurrentPrice([
    moneywagon.Bitstamp
    moneywagon.BTCE, // switched order from last example
]);

console.log(service.get('btc', 'usd'));
```

    [377.22, 'bitstamp']
