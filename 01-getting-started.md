# Getting Started

All HTTP requests must contain the following headers:

* BB-PARTNER-ID
* BB-ACCESS-KEY
* BB-ACCESS-SIGN
* BB-TIMESTAMP


Once a `Partnership` is formed then the necessary details will be sent.

## Partnership

When a `Partnership` is formed, an instance of a `Partner`, `Client`, and `ClientCredential` will be formed.

### Partner

The `id` of the instance of `Partner` is what we send over in the `BB-PARTNER-ID` request header.

### Client

An instance of a `Partner` might want to create multiple instances of `Client` for various reasons. For example it might make sense to create an instance of a `Client` on a device specific level (iOS, Android, Web) or on a purpose level (development, testing, production).

#### Client Credential

Every instance of a `Client` is partnered up with an instance of a `Client Credential`. The `api_key` of the instance of `Client Credential` is what we send over in the `BB-ACCESS-KEY` request header.

With the `secret` of the instance of `Client Credential`, we can [create a signature](https://docs.bitbutter.com/#signing-a-message) for the `BB-SIGNATURE` request header.

## Create a User

### Get Users
