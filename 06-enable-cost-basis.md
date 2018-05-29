# Enabling Cost Basis 

All `ledger`, `transfers`, and `trades` routes can enable cost basis (native historical prices). Historical prices are accurate to within 5 minute of the recorded time of the transaction. Applied to fee, base, size, quote. Basis can then be used to calculate capital gains when you later sell/trade/purchase etc.

## Endpoints

The current endpoints that cost basis parameter can be enabled:

* get user ledger `/v1/users/{{USER_ID}}/ledger`

* get connected exchange ledger `/v1/connected-exchanges/{{CONNECTED_EXCHANGE_ID}}/ledger`

* get connected exchange trades `/v1/connected-exchanges/{{CONNECTED_EXCHANGE_ID}}/trades`

* get connected exchange transfers `/v1/connected-exchanges/{{CONNECTED_EXCHANGE_ID}}/transfers`

* get connected address ledger `/v1/connected-addresses/{{CONNECTED_ADDRESS_ID}}/ledger`

## Enable

```
?cost_basis=true
```

The default value for `cost_basis` is false.

## Sample

```javascript 
    {
        "connectable": {
            "id": "3908f25e-4b6c-46cd-9b78-34864c998b42",
            "name": "Binance",
            "type": "Exchange"
        },
        "details": {
            "subtitle": "Using Binance Bitcoin account",
            "title": "Bought Bitcoin"
        },
        "id": "63c211d-8eb3-43b8-b62c-0o90ce76558a",
        "time": "2017-11-18T04:47:10.284Z",
        "transaction_type": "buy",
        "base": {
            "name": "Bitcoin",
            "size": "0.00135600",
            "symbol": "BTC",
            "price_per_unit": "19030.947",
            "cost_basis": "25.806"
        },
        "size": {
            "name": "Bitcoin",
            "size": "0.00135600",
            "symbol": "BTC",
            "price_per_unit": "19030.947",
            "cost_basis": "25.806"
        },
        "quote": {
            "name": "Tether",
            "size": "-25.52402868",
            "symbol": "USDT",
            "price_per_unit": "0.988",
            "cost_basis": "-25.218"
        },
        "fee": {
            "name": "Bitcoin",
            "size": "0.00000136",
            "symbol": "BTC",
            "price_per_unit": "19030.947",
            "cost_basis": "0.026"
        }
    }
```
