# Addresses

Users can connect their wallets by providing the address.

## Supported Addresses

* Bitcoin

* Ethereum (ERC 20 tokens displayed in balances)

## Connecting an Address

To connect an address we make a POST request to this url:

```
{{ENDPOINT}}/v1/connected-addresses
```

Our body for hte request might look something like the following.

```
{ 
  "asset_id": "{{ETHEREUM_ASSET_ID}}",
  "address": "{{ETHEREUM_ADDRESS}}",
  "user_id": "{{USER_ID}}"
}
```

## Balances

Once an address is connected, we can get the current balances by making a request to `get connected address balances` route. The route takes in a path parameter of `CONNECTED_ADDRESS_ID` which our Postman automatically set when we connected the address.

```
{{ENDPOINT}}/v1/connected-addresses/{{CONNECTED_ADDRESS_ID}}/balances
```

## Ledger

We can get the ledger of the connected address by making a request to `get connected address ledger`.

```
{{ENDPOINT}}/v1/connected-addresses/{{CONNECTED_ADDRESS_ID}}/ledger
```

## Differences between blockchains

Depending on the cryptocurrency, the transaction data might differ in structure.

### Balances

The main difference between the balances of Bitcoin and Ethereum is that an Ethereum address can also hold other ERC 20 tokens.

### Ledger

Bitcoin transactions have `inputs` and `outputs` while Ethereum addresses have `from` and `to` properties.


## Sync

To update transaction history with recent activities, we can make a GET request to `sync connected address` route.

```
{{ENDPOINT}}/v1/connected-addresses/{{CONNECTED_ADDRESS_ID}}/sync
```