# Getting Started

Welcome to Bitbutter guides! Let's get started by first navigating to [https://docs.bitbutter.com](https://docs.bitbutter.com). On the top right corner, click the orange button that says "Run in Postman."

<img width="720px" src="https://i.imgur.com/SGNKqpd.jpg">

Go ahead and install Postman if you haven't already. Postman will help us get started with the API right away. We have built in the pre-request signatures that are required for each request as well as populating the correct environment variables.

## Postman Interface Overview

Let's quickly go over the Postman interface. There are three main views to pay attention to: Routes View, Main View, and the Environment View.

### Routes View

<img width="720px" src="https://i.imgur.com/I1Ag0fI.jpg">

The Routes View lists out the routes provided by our API.

### Main View

<img width="720px" src="https://i.imgur.com/5SKvekX.jpg">

The Main View changes whenever we click a route frome the Routes View. We can interact with the specified route by changing body and query parameters and sending requests to the specified endpoint.

### Environment View

<img width="720px" src="https://i.imgur.com/YY5SYaz.jpg">

The Environment View is where we can set variables that we can access in our routes. We have prepopulated some of the variables for you such as `ENDPOINT` and `PARTNERSHIP_ID`.

<img width="720px" src="https://i.imgur.com/tsjruz2.jpg">

By click on the eye icon and clicking 'Edit', we can add, modify and delete environment variables.

## Bitbutter API

For administrative tasks such as creating a user, seeing all users, and deleting a user, we need partner credentials. These administrative tasks are part of the Partner API. The User API are endpoints that allow users to connect cryptocurrency exchanges and addresses and display them. Before the User API can be used, a user has to be created through the Partner API.

### User API

To access the User API, we need valid user credentials. When a user is created, an `api_key` and `secret` are returned. These credentials are used to restrict access of the user's connected accounts strictly to them. All endpoints in the User API can be accessed through partner credentials. The user credentials should be stored on the user's client device. These credentials can then be used to sign requests from the client.
 
### Partner API

We need valid partner credentials to access the Partner API. It is essential that these credentials are not stored on the client. The client should only store user credentials because partner credentials give access to admin level routes such as deleting a user. 

## Creating a User

Let's navigate to the [Partner API](https://documenter.getpostman.com/view/3815526/RVu2kpi9) and make our first requests using Postman

<img width="720px" src="https://i.imgur.com/YYqvmTb.jpg">

### Headers

Let's click on the `create user` route on the Routes View. We will get a response with the user credentials that we can now use to access the User API.

<img width="720px" src="https://i.imgur.com/gyezu13.jpg">

Let's take a quick look at the Headers tab in the Main View to get a better understanding of how we were authenticated to access the endpoint.

<img width="720px" src="https://i.imgur.com/rGpzU4p.jpg">

These are the four required headers for accessing the Partner API. 

### Authentication

The signature for partner routes and User routes are created the same way. The signature needs four pieces of information to create: timestamp, method, requestPath and body. The method has to be all uppercase (i.e. "GET").

 We are creating the signature using Postman and the credentials provided in the Environment View. The signature algorithm is like the following in JavaScript.

```javascript
import * as crypto from 'crypto';

const secret = '5J6AJYkZJXw97YgW...';

//  Number of milliseconds elapsed since January 1, 1970 00:00:00 UTC.
const timestamp = Date.now();
const method = 'POST';
const requestPath = '/users';
const body = '';

// 1. Concatentate required parts into one string
//    If body is an object, stringify (remove all white spaces) 
const prehash = timestamp + method + requestPath + JSON.stringify(body);

// 2. Base64 decode string
const key = new Buffer(secret, 'base64');

// 3. Create sha256 hmac with the base64 decoded string
const hmac = crypto.createHmac('sha256', key);

// 4. Sign with the sha256 hmac and base64 encode the result
hmac.update(prehash).digest('base64');
```

## Connecting an Exchange

Now that we created a user, let's connect an exchange account to it. We currently support connection on Binance, Bittrex, Coinbase, GDAX, Kraken and Poloniex. For our example we will be connecting Binance. Go ahead and navigate to the the [User API](https://docs.bitbutter.com) and then click on the the `connect exchange` route from the Routes View.

<img width="720px" src="https://i.imgur.com/hkAwntb.jpg">

### Body Parameters

Let's take a look at what body parameters we are sending up.

<img width="720px" src="https://i.imgur.com/R7l2gvl.jpg">

We have to provide the necessary values for `BINANCE_API_KEY`, `BINANCE_SECRET`, and `BINANCE_EXCHANGE_ID`. We have populated the `BINANCE_EXCHANGE_ID` but you'll have to update the values for the API key and secret. The `USER_ID` environment was automatically set by Postman when we initially created the user.

If you want to try another exchange, you can modify the body parameters like the following for corresponding exchange.

#### Binance

```
{ 
  "credentials": { 
    "api_key": "{{BINANCE_API_KEY}}",
    "secret": "{{BINANCE_SECRET}}"
  },
  "exchange_id": "{{BINANCE_EXCHANGE_ID}}",
  "user_id": "{{USER_ID}}"
}
```

#### Bittrex

```
{ 
  "credentials": { 
    "api_key": "{{BITTREX_API_KEY}}",
    "secret": "{{BITTREX_SECRET}}"
  },
  "exchange_id": "{{BITTREX_EXCHANGE_ID}}",
  "user_id": "{{USER_ID}}"
}
```

#### Coinbase

```
{ 
  "credentials": { 
    "api_key": "{{COINBASE_API_KEY}}",
    "secret": "{{COINBASE_SECRET}}"
  },
  "exchange_id": "{{COINBASE_EXCHANGE_ID}}",
  "user_id": "{{USER_ID}}"
}
```

#### GDAX

```
{ 
  "credentials": { 
    "api_key": "{{GDAX_API_KEY}}",
    "secret": "{{GDAX_SECRET}}"
    "password": "{{GDAX_PASSWORD}}"
  },
  "exchange_id": "{{GDAX_EXCHANGE_ID}}",
  "user_id": "{{USER_ID}}"
}
```

#### Kraken

```
{ 
  "credentials": { 
    "api_key": "{{KRAKEN_API_KEY}}",
    "secret": "{{KRAKEN_SECRET}}"
  },
  "exchange_id": "{{KRAKEN_EXCHANGE_ID}}",
  "user_id": "{{USER_ID}}"
}
```

#### Poloniex

```
{ 
  "credentials": { 
    "api_key": "{{POLONIEX_API_KEY}}",
    "secret": "{{POLONIEX_SECRET}}"
  },
  "exchange_id": "{{POLONIEX_EXCHANGE_ID}}",
  "user_id": "{{USER_ID}}"
}
```

### Headers

<img width="720px" src="https://i.imgur.com/xkWZF21.jpg">

Let's take a look at the headers that we are providing to this endpoint.

#### User Credentials

All User API HTTP requests must contain the following headers:

* BB-USER-ID: The user id

* BB-ACCESS-KEY: The user api key

* BB-ACCESS-SIGN: Base64 encoded signature (see Authentication)

* BB-TIMESTAMP: A UTC timestamp for your request (number of milliseconds elapsed since January 1, 1970 00:00:00 UTC)

#### Partner Credentials

All Partner API HTTP requests must contain the following headers:

* BB-PARTNER-ID: The partner id

* BB-ACCESS-KEY: The partner api key

* BB-ACCESS-SIGN: Base64 encoded signature (see Authentication)

* BB-TIMESTAMP: A UTC timestamp for your request (number of milliseconds elapsed since January 1, 1970 00:00:00 UTC)

## Get Connected Exchanges

<img width="720px" src="https://i.imgur.com/3t5lGih.jpg">

Now let's navigated to the `get connected exchanges` route to see if the exchange of our choice has been connected. We should see a response like the following.

The `sync_progress` indicates the progress of the sync from a range of 1 to 100, with 100 being complete. The `synced_at` timestamp indicates when the last successful sync was.

## Get User Balances

<img width="720px" src="https://i.imgur.com/YM6bAzV.jpg">

Once the sync is completed, we can verify that the sync was successful by navigating to the `get user balances` route and making a request.

## Get User Ledger

<img width="720px" src="https://i.imgur.com/CHNvjsC.jpg">

We can get the ledger (history of withdrawals, deposits, and trades) through the `get user ledger` route as well.
