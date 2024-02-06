---
description: How to use BankTransfer to submit a payout in Colombia.
---

# BankTransfer

{% swagger method="post" path=" /api/payout" baseUrl="https://sandbox.transfersmile.com" summary="Submit a payout by Bank Transfer in Colombia" %}
{% swagger-description %}
This endpoint allows you to submit a payout by BankTransfer in Colombia.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" required="true" type="string" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="AppId" type="string" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Authorization" type="string" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" required="true" type="string" name="name" %}
Beneficiary's name, length must between 5 and 100
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="phone" required="true" %}
Beneficiary's phone

\- 0 \~ 15 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="email" required="true" %}
Beneficiary 's email
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="bank_code" required="true" %}
Bank code, see [_**bank list​**_](../../bank-code/bank-in-colombia.md)
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="document_id" required="true" %}
Beneficiary document id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_type" type="string" required="true" %}
Beneficiary [_**document type**_](banktransfer.md#account-type), should be one of CC, CE, PEP
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="account" required="true" %}
Account

\- 8 \~ 18 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="account_type" required="true" %}
Should be one of CHECKING, SAVINGS
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="method" required="true" %}
Fixed Value: BankTransfer
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="custom_code" required="true" %}
Merchant's order id

\- Max.50 -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="fee_bear" required="true" %}
One of \[beneficiary | merchant]
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="string" required="true" %}
Payout amount, should be an Integer.

\- Min 1, Max 20,000,000 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount_type" type="string" required="false" %}
Specify the amount value is fixed for merchant or beneficiary\
\- One of: source\_amount, arrival\_amount(default) -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" type="string" required="true" %}
Merchant's account currency

\-  supported: USD, GBP, EUR, COP -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" type="string" required="true" %}
Beneficiary's account currency.

\- Fixed Value: COP -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where pagsmile will callback to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additionl_remark" type="string" required="true" %}
Additional Remark\
\- Max Length: 40 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" type="string" required="true" %}
Fixed value: COL, for Colombia
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="success" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQBC",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "100",
        "arrival_currency": "COL",
        "source_amount": "0.07",
        "source_currency": "USD",
        "status": "IN_PROCESSING"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="bad request" %}
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
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="unautorized" %}
```javascript
{
    "code": 4004003,
    "msg": "permission denied",
    "time": 1637224716,
    "data": {
        ... ...
    }
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="fee not configured" %}
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
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="balance insufficient" %}
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
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="system error" %}
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
{% endswagger-response %}
{% endswagger %}

## Example

```
curl --location --request POST 'https://sandbox.transfersmile.com/api/payout' \
--header 'AppId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "name" : "GUILHERME ****** SOUZA",
    * "phone" : "468****068", // phone is required
    * "email" : "g******me@gmail.com", // email is required
    * "bank_code": "007", // Bancolombia
    * "account" : "002194002546406543", // just for test in sandbox
    * "account_type" : "CHECKING",
    * "document_id" : "123456789", // just for test in sandbox, don't use this in production.
    * "document_type" : "CC",
    * "method" : "BankTransfer",
    * "custom_code" : "custom_code9982674851738108",
    * "fee_bear" : "merchant",
    * "amount" : "100", //Amount should be an integer, like 1.00 is not available.
    * "source_currency" : "COP",
    * "arrival_currency" : "COP",
    * "notify_url" : "https://notify.url",
    * "additional_remark" : "pagsmile payout test",
    * "country": "COL"
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

## Document Type

| Name | Length          | Type       |
| ---- | --------------- | ---------- |
| CC   | Between 6 to 10 | numeric    |
| CE   | up to 12        | characters |
| PEP  | up to 15        | numeric    |

## Example of Account

| Account Type | Account              | Description   |
| ------------ | -------------------- | ------------- |
| CHECKING     | 1\*\*\*\*\*\*\*\*\*6 | 9 - 18 digits |
| SAVINGS      | 2\*\*\*\*\*\*\*\*\*8 | 9 - 18 digits |
