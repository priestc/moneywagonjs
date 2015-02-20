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

Most common cryptocurrencies and most fiat currencies are supported.

### Custom service fallback order:

```js
var service = new moneywagon.CurrentPrice([
    moneywagon.BTCE,
    moneywagon.Bitstamp
]);

service.getCurrentPrice('btc', 'usd', function() {
    console.log("One bitcoin is worth", price, "US Dollars according to", source);
);
```

    One bitcoin is worth 377.2 US Dollars according to btce

The first service is tried first, if the first service returns an error, the second service is tried.

```js
var service = new moneywagon.CurrentPrice([
    moneywagon.Bitstamp
    moneywagon.BTCE, // switched order from last example
]);

service.getCurrentPrice('btc', 'usd', function() {
    console.log("One bitcoin is worth", price, "US Dollars according to", source);
);
```

    One bitcoin is worth 378.0 US Dollars according to bitstamp
