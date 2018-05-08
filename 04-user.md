# User

A user can connect multiple exchanges and wallets. The user endpoint is great for seeing an aggregated view.

## Create user

The creation of the user requires partner credentials. The Partner API is further explained in the next document. This means that the creation of the user should not happen on the user's client because partner credentials should never be stored on the user's device. A sample backend that handles the creation of the user without exposing the partner credentials to every user can be found in here: [https://github.com/BitbutterHQ/server](https://github.com/BitbutterHQ/server).

## Balances

If we want to see the balances of the user across all connected exchanges and wallets we can make a request to `get user balances` route.

```
{{ENDPOINT}}/v1/users/{{USER_ID}}/balances
```

## Ledger

To see the entire transaction history of a user across all connected accounts, we can make a request to `get user ledger` route.

```
{{ENDPOINT}}/v1/users/{{USER_ID}}/ledger
```
