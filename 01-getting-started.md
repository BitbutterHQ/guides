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

const timestamp = Date.now() / 1000;
const method = 'POST';
const requestPath = '/users';
const body = '';

// 1. Concatentate required parts into one string
const prehash = timestamp + method + requestPath + body;

// 2. Base64 decode string
const key = new Buffer(secret, 'base64');

// 3. Create sha256 hmac with the base64 decoded string
const hmac = crypto.createHmac('sha256', key);

// 4. Sign with the sha256 hmac and base64 encode the result
hmac.update(prehash).digest('base64');
```
