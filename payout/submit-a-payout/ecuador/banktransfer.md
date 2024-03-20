---
description: How to use Bank Transfer to submit a payout in Ecuador.
---

# BankTransfer

## Submit a payout by Bank Transfer in Ecuador.

<mark style="color:green;">`POST`</mark> `https://sandbox.transfersmile.com/api/payout`

This endpoint allows you to submit a payout by Bank Transfer in Ecuador.

#### Headers

| Name                                            | Type   | Description                         |
| ----------------------------------------------- | ------ | ----------------------------------- |
| Content-Type<mark style="color:red;">\*</mark>  | string | application/json; charset=UTF-8     |
| AppId<mark style="color:red;">\*</mark>         | string | Your App ID in payout platform.     |
| Authorization<mark style="color:red;">\*</mark> | string | SHA256($sorted\_params + $app\_key) |

#### Request Body

| Name                                                 | Type   | Description                                                                                                                   |
| ---------------------------------------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------- |
| name<mark style="color:red;">\*</mark>               | string | Beneficiary's name, length must between 5 and 100                                                                             |
| amount\_type                                         | string | <p>Specify the amount value is fixed for merchant or beneficiary</p><p>- One of: source_amount, arrival_amount(default) -</p> |
| amount<mark style="color:red;">\*</mark>             | string | <p>Payout amount </p><p>- Min 0.01, Max 500,000 -</p>                                                                         |
| fee\_bear<mark style="color:red;">\*</mark>          | string | One of \[beneficiary \| merchant]                                                                                             |
| custom\_code<mark style="color:red;">\*</mark>       | string | Merchant's order id.                                                                                                          |
| method<mark style="color:red;">\*</mark>             | string | Fixed Value: BankTransfer                                                                                                     |
| document\_type<mark style="color:red;">\*</mark>     | string | Beneficiary document type, should be one of CEDULA, RUC, PAS.                                                                 |
| document\_id<mark style="color:red;">\*</mark>       | string | Beneficiary document id                                                                                                       |
| account\_type<mark style="color:red;">\*</mark>      | string | Should be one of CHECKING, SAVINGS                                                                                            |
| account<mark style="color:red;">\*</mark>            | string | <p>Account</p><p>- 10 ~ 20 digits -</p>                                                                                       |
| bank\_code<mark style="color:red;">\*</mark>         | string | Bank code, see [_**bank list**_](../../bank-code/bank-in-ecuador.md)                                                          |
| email                                                | string | Beneficiary's email                                                                                                           |
| phone                                                | string | <p>Beneficiary's phone</p><p>- 0 ~ 15 digits -</p>                                                                            |
| additional\_remark<mark style="color:red;">\*</mark> | string | <p>Additional Remark<br>- Max Length: 40 - </p>                                                                               |
| notify\_url<mark style="color:red;">\*</mark>        | string | Where pagsmile will callback to                                                                                               |
| arrival\_currency<mark style="color:red;">\*</mark>  | string | <p>Beneficiary's account currency.</p><p>- Fixed Value: USD -</p>                                                             |
| source\_currency<mark style="color:red;">\*</mark>   | string | <p>Merchant's account currency</p><p>- supported: USD, GBP, EUR -</p>                                                         |
| country<mark style="color:red;">\*</mark>            | string | Fixed value: ECU, for Ecuador.                                                                                                |

{% tabs %}
{% tab title="200: OK success" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQBEC",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "100",
        "arrival_currency": "PEN",
        "source_amount": "0.07",
        "source_currency": "USD",
        "status": "IN_PROCESSING"
    }
}
```
{% endtab %}

{% tab title="400: Bad Request bad request" %}
```javascript
{
    "code": 4001000,
    "msg": "invalid parameter",
    "time": 1637224716,
    "data": {
        "err": "error detail message"
    }
}
```
{% endtab %}

{% tab title="401: Unauthorized unauthorized" %}
```javascript
{
    "code": 4004003,
    "msg": "permission denied",
    "time": 1637224716,
    "data": {}
}
```
{% endtab %}

{% tab title="500: Internal Server Error system error" %}
```javascript
{
    "code": 5001000,
    "msg": "system error",
    "time": 1637224716,
    "data": {
        "err": "error detail message"
    }
}
```
{% endtab %}

{% tab title="500: Internal Server Error fee not configured" %}
```javascript
{
    "code": 5001003,
    "msg": "fee not configured",
    "time": 1637224716,
    "data": {
        ... ...
    }
}
```
{% endtab %}

{% tab title="500: Internal Server Error balance insufficient" %}
```javascript
{
    "code": 5001102,
    "msg": "balance insufficient",
    "time": 1637224716,
    "data": {
        ... ...
    }
}
```
{% endtab %}
{% endtabs %}

## Example

```
curl --location --request POST 'https://sandbox.transfersmile.com/api/payout' \
--header 'AppId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "name" : "GUILHERME ****** SOUZA",
      "phone" : "468****068",
      "email" : "g******me@gmail.com",
    * "bank_code": "0001", // Banco Central del Ecuador
    * "account" : "00219400254640654321", // just for test in sandbox
    * "account_type" : "CHECKING",
    * "document_id" : "1234567890001", // just for test in sandbox, don't use this in production.
    * "document_type" : "PAS",
    * "method" : "BankTransfer",
    * "custom_code" : "custom_code9982674851738108",
    * "fee_bear" : "merchant",
    * "amount" : "100",
    * "source_currency" : "USD",
    * "arrival_currency" : "USD",
    * "notify_url" : "https://notify.url",
    * "additional_remark" : "pagsmile payout test",
    * "country": "ECU"
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

## Example of Document

| Document Type | Document ID           | Description                       |
| ------------- | --------------------- | --------------------------------- |
| CEDULA        | 01\*\*\*\*\*\*\*6     | 10 digits                         |
| PAS           | 02\*\*\*\*\*\*\*\*\*8 | 13 digits, always start with 001. |
| RUC           | 03\*\*\*\*\*\*\*\*\*9 | 13 digits, always start with 001. |

## Example of Account

| Bank                   | Bank Code | Description                            |
| ---------------------- | --------- | -------------------------------------- |
| Banco Pichincha C.A.   | 0010      | The account must contain 10 digits     |
| Banco de Guayaquil S.A | 0017      | The account must contain max 10 digits |
| Others                 |           | 7 - 20 digits                          |
