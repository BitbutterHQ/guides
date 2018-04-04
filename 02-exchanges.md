# Exchanges

Users can connect their cryptocurrency exchange accounts by providing a read-only API key.

## Supported Exchanges

* Binance

* Bittrex

* Coinbase

* GDAX

* Kraken

* Poloniex

## Upcoming Exchanges

* Coinbase OAuth

* Kucoin (waiting for read only implementation)

* Gemini

* CEX

* Bitstamp

## Connecting an Exchange

To connect an exchange, navigate to `connect exchange` in Postman. This is going to be a `POST` request where we send along body parameters where we provide the exchange credentials as well as the id of the exchange.

```javascript
{ 
  "credentials": { 
    "api_key": "{{BINANCE_API_KEY}}",
    "secret": "{{BINANCE_SECRET}}"
  },
  "exchange_id": "{{BINANCE_EXCHANGE_ID}}",
  "user_id": "{{USER_ID}}"
}
```

We can get the id of the exchange that we want by first making a request to `get all exchanges`. This will return a list of exchanges and then we can choose the exchange that we want to connect to.

## Connected Exchange

Once an exchange is connected, it becomes a connected exchange. We can see all the exchanges users have connected by making a request to `get user connected exchanges` route.

```javascript
{
    "connected_exchanges": [
        {
            "exchange": {
                "id": "a55b29b9-722b-4e38-a30f-96319ed90f02",
                "name": "Binance"
            },
            "id": "a2653366-80a6-41bf-bf86-289e9e500950",
            "sync_progress": 100,
            "synced_at": "2018-04-04T00:06:57.265Z"
        }
    ]
}
```

### Balances

Once an exchange is connected, we can get the current balances by making a request to `get connected exchange balances` route. The route takes in a path parameter of `CONNECTED_EXCHANGE_ID` which our Postman automatically set when we connected the exchange.

```
{{ENDPOINT}}/v1/connected-exchanges/{{CONNECTED_EXCHANGE_ID}}/balances
```

If we want to change this, we can first make a request to `get user connected exchanges` to get the id of the connected exchange we want, and then modifying the `CONNECTED_EXCHANGE_ID` in the Environment View.

```javascript
[
    {
        "connectable": {
            "id": "a2653366-80a6-41bf-bf86-289e9e500950",
            "name": "Binance",
            "type": "Exchange"
        },
        "id": "6e324935-1f00-4218-8b81-a3a97ecbc21e",
        "name": "BTC",
        "asset": {
            "id": "81f233c4-6dc1-4b91-a38c-2a697f504e5e",
            "name": "Bitcoin",
            "size": "0.00000000",
            "symbol": "BTC"
        }
    },
    // ...
]
```

### Ledger

We can get the ledger of a connected exchange as well. A ledger is a history of all deposits, withdrawals, and trades within the connected exchange. We can get the ledger by makign a request to `get connected exchange ledger` route.

```
{{ENDPOINT}}/v1/connected-exchanges/{{CONNECTED_EXCHANGE_ID}}/ledger
```

Similar to the balances route, we need to provide the right value to the `CONNECTED_EXCHANGE_ID` environment variable.

```javascript
[
    {
        "connectable": {
            "id": "a2653366-80a6-41bf-bf86-289e9e500950",
            "name": "Binance",
            "type": "Exchange"
        },
        "details": {
            "subtitle": "From Ethereum address",
            "title": "Received Ethereum"
        },
        "id": "8a31edce-4033-4a83-af20-3937991e9868",
        "time": "2017-12-18T05:59:10.000Z",
        "transaction_type": "exchange_deposit",
        "from": {
            "address": "0x9d2ec5f7d3e47bae180cd9214c4e2da2634335c3",
            "asset": {
                "name": "Ethereum",
                "size": "0.00700000",
                "symbol": "ETH"
            },
            "name": null
        },
        "size": {
            "name": "Ethereum",
            "size": "0.00500000",
            "symbol": "ETH"
        }
    }
]
```
