# moneywagonjs
Multi-blockchain service API client library for javascript

This library is a direct port of the python library of the same name.

## Usage

Place the moneywagon javascript file into your page:

    <script src="moneywagon.min.js"></script>

Henceforth, your page will have access to the moneywagon API which is as follows:

### moneywagon.getCurrentPrice

Call to the getCurrentPrice function will make an ajax call to some blockchain
service API, the result is passed onto the callback function.

```js
moneywagon.getCurrentPrice('btc', 'usd', function(price, source) {
    console.log("One bitcoin is worth", price, "US Dollars according to", source);
});
```

    One bitcoin is worth 391.324 US Dollars according to bitstamp

The first argument is the crypto price, the second argument is the fiat price.
`source` is the string of the service used, `price` is the conversion ratio.

```js
moneywagon.getCurrentPrice('ltc', 'rur', function(price, source) {
    console.log("One Litecoin is worth" price, "Russian Rubles, according to", source);
});
```

    One Litecoin is worth 169.54116322 Russian Rubles, according to cryptonator

### Custom service fallback order:

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
