---
title: Payment Service API

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php

toc_footers:
  - <a href='#'>Documentation powered by Community Brands R&D</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Payment Service API! You can use Payment Service API to access Transactions API endpoints, which can get information about various transaction in our Payment Service database.

We have language bindings in Shell and PHP! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

How to set up the project?

Pull `paymnt-service-api` from beanstalk and follow the README.md file.

# Authentication

Payment Service API uses token-based authentication. 

As an authentication system uses Symfony security Guard bundle with standard JWT (JSON Web Token) to generate a token.

`1. User Requests Access with Username / Password.`

`2. API validates credentials.`

`3. API provides a signed token to the client.`

`4. The client stores the token and sends it along with every request.`

`5. API verifies token and responds with data.`


![Auth Diagram](auth_diagram.png)

## Get Token endpoint

> Get Access Token

```shell

curl -X POST --user username:password http://127.0.0.1:8000/api/v1/tokens

```

```php
<?php
$response = $this->client->post('/api/v1/tokens', [
            'auth' => ['username', 'password']
        ]);
        
$data = json_decode($response->getBody(), true);
?>
```

> Make sure to replace `username` and `password` with your username and password.

This endpoint exchanges a username and password for JWT Token.

### HTTP Request

`POST http://localhost/api/v1/tokens`

<aside class="notice">
You must replace <code>localhost</code> with the correct environment.
</aside>

## Additional Documentation:
### `Symfony Guard Authentication:`

* [Guard component](https://symfony.com/components/Guard)

* [How to Create a Custom Authentication System with Guard](https://symfony.com/doc/current/security/guard_authentication.html)

### `JWT`
*[JWT Official Site ](https://jwt.io/)

### `Token Based Authentication`
*[Token Based Authentication Article](https://scotch.io/tutorials/the-ins-and-outs-of-token-based-authentication)


# Transactions

## Get All Transactions

```shell
`curl -H "Authorization: Bearer <yourtoken>" http://127.0.0.1:8000/api/v1/transactions`
```

```php
<?php
$response = $this->client->get('/api/v1/transactions', [
            'body' => '[]',
            'headers' => [
                'Authorization' => 'Bearer '.'<yourtoken>',
            ]
        ]);

$data = json_decode($response->getBody(), true);

?>
```
This endpoint retrieves all transactions.

### HTTP Request

`GET http://127.0.0.1:8000/api/v1/transactions`

### Header Authorization

Parameter | Description
--------- |  -----------
$headers['Authorization'] = 'Bearer '.$token;     | Authorization token

<aside class="success">
Remember — to get transactions you have to be authenticated!
</aside>

## Transactions Response

Check out the JSON Response on the right

`JSON format on the right` all parameters are wrapped in data.

> The above command returns JSON structured like this:

```json
 { "data": 
   {
     "created": "2018-07-17T18:06:41+00:00",
     "modified": "2018-07-17T18:06:41+00:00",
     "completed": "2018-07-17T18:06:41+02:00",
     "isComplete": true,
     "amount": 5,
     "amountTotal": 5,
     "currencyCode": "USD",
     "customerId": 9,
     "fullName": "FirstName LastName",
     "billingInformation": "123 Test Ave Test MA United States 11111",
     "creditCardNumber": null,
     "bankName": "WELLS FARGO BANK NA (MINNESOTA)",
     "bankRoutingNumber": "091000019",
     "achAccountNumber": "0123",
     "achAccountType": "checking",
     "organizationId": "noa",
     "uuid": "1fef6602-89ec-11e8-9ac4-60030889a1c8",
     "orderId": "BILLPAY-F08421-155-690-5b4e3023870fd-2018-07-17_18:06:40",
     "transactionNumber": "4199768865",
     "referenceNumber": "",
     "transactionLog": "response=1&responsetext=SUCCESS&authcode=123456&transactionid=4199768865&avsresponse=&cvvresponse=&orderid=&type=&response_code=100&customer_vault_id=1665123394",
     "applicationId": "BILLPAY",
     "provider": "nmi_direct_post",
     "ipSrc": "127.0.0.1:63418",
     "browser": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36",
     "scheduledPaymentId": null,
     "isServiceFee": false,
     "isReverted": false,
     "adminFeeId": null,
     "serviceFeeId": null,
     "adminFeeAmount": null
  }
}
