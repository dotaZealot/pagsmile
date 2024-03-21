---
description: Where to use Vita wallet to submit a payout in Chile.
---

# Wallet

## Submit a payout by Wallet in Chile

<mark style="color:green;">`POST`</mark> `https://sandbox.transfersmile.com/api/payout`&#x20;

This endpoint allows you to submit a payout by e-Wallet in Chile.

#### Headers

| Name                                            | Type   | Description                         |
| ----------------------------------------------- | ------ | ----------------------------------- |
| Content-Type<mark style="color:red;">\*</mark>  | string | application/json; charset=UTF-8     |
| AppId<mark style="color:red;">\*</mark>         | string | Your App ID in payout platform      |
| Authorization<mark style="color:red;">\*</mark> | string | SHA256($sorted\_params + $app\_key) |

#### Request Body

| Name                                                 | Type   | Description                                                                                                                |
| ---------------------------------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------- |
| name                                                 | string | <p>Beneficiary's name</p><p>- Min.5 Max.100 -</p>                                                                          |
| phone                                                | string | <p>Beneficiary's phone.</p><p>- 0 ~ 15 digits -</p>                                                                        |
| email                                                | string | <p>Beneficiary's email</p><p>- Max.64 -</p>                                                                                |
| account<mark style="color:red;">\*</mark>            | string | <p>Beneficiary Vita account.</p><p>- 0 ~ 64 chars -</p>                                                                    |
| account\_type<mark style="color:red;">\*</mark>      | string | Fixed Value: EMAIL                                                                                                         |
| document\_id                                         | string | Beneficiary document id                                                                                                    |
| document\_type                                       | string | Beneficiary document type                                                                                                  |
| methd<mark style="color:red;">\*</mark>              | string | Fixed Value: WALLET                                                                                                        |
| channel<mark style="color:red;">\*</mark>            | string | Fixed Value: Vita                                                                                                          |
| custom\_code<mark style="color:red;">\*</mark>       | string | <p>Merchant's order id</p><p>- Max.50 -</p>                                                                                |
| fee\_bear<mark style="color:red;">\*</mark>          | string | One of \[beneficiary \| merchant]                                                                                          |
| amount<mark style="color:red;">\*</mark>             | string | <p>Payout amount, should be an Integer.</p><p>- Min 5000, Max 2,000,000 - </p>                                             |
| amount\_type                                         | string | <p>Specify the amount value is fixed for merchant or beneficiary<br>- One of: source_amount, arrival_amount(default) -</p> |
| arrival\_currency<mark style="color:red;">\*</mark>  | string | <p>Beneficiary's account currency.</p><p>- Fixed Value: CLP -</p>                                                          |
| source\_currency<mark style="color:red;">\*</mark>   | string | <p>Merchant's account currency</p><p>- supported: USD, GBP, EUR, CLP -  </p>                                               |
| notify\_url<mark style="color:red;">\*</mark>        | string | Where pagsmile will callback to                                                                                            |
| additional\_remark<mark style="color:red;">\*</mark> | string | <p>Additional Remark<br>- Max length: 40 - </p>                                                                            |
| country<mark style="color:red;">\*</mark>            | string | <p>Beneficiary's Country</p><p>- Fixed Value: CHL - </p>                                                                   |

{% tabs %}
{% tab title="200: OK submit successfully" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQWCL",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "100",
        "arrival_currency": "CLP",
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
    "data": {}
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
    "data": {}
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

## Example of Document

{% hint style="info" %}
* RUT / RUN numbers have eight digits, plus a verification digit, and are generally written in this format: xxxxxxxx-z. Z can be a digit or the letter K. For example 3\*\*\*\*\*\*7-K,  7\*\*\*\*\*\*8-5. **Only send alphanumeric values in the API**, like 3\*\*\*\*\*\*7K.
* For individuals, RUT is the same as RUN. For businesses, they only have RUT.
{% endhint %}

<table><thead><tr><th width="176">Document Type</th><th width="160">Document ID</th><th width="135">Description</th><th width="405"></th><th></th></tr></thead><tbody><tr><td>RUT</td><td>7******85</td><td>9 digits</td><td>A RUT <em>(Rol Único Tributario)</em> is the individual tax ID number </td><td></td></tr><tr><td>RUN</td><td>7******85</td><td>9 digits</td><td>A RUN <em>(Rol Único Nacional)</em> is a unique identification number given to every Chilean resident, foreign resident, and anyone who stays in Chile on anything other than a tourist visa</td><td></td></tr></tbody></table>

## Example

```
curl --location --request POST 'https://sandbox.transfersmile.com/api/payout' \
--header 'AppId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
      "name" : "GUILHERME ****** SOUZA",
      "phone" : "468****068",
      "email" : "g******me@gmail.com",
    * "account" : "g******me@gmail.com",
    * "account_type" : "EMAIL",
      "document_id" : "************",
      "document_type" : "***",
    * "method" : "WALLET",
    * "channel" : "Vita",
    * "custom_code" : "custom_code9982674851738108",
    * "fee_bear" : "merchant",
    * "amount" : "100", //Amount should be an integer, like 1.00 is not available.
    * "source_currency" : "CLP",
    * "arrival_currency" : "CLP",
    * "notify_url" : "https://notify.url",
    * "additional_remark" : "pagsmile payout test",
    * "country": "CHL"
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}
