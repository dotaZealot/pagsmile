---
description: How to use Bank Transfer to submit a payout in Peru.
---

# BankTransfer

{% swagger method="post" path="/api/payout" baseUrl="https://sandbox.transfersmile.com" summary=" Submit a payout by Bank Transfer in Peru." %}
{% swagger-description %}
This endpoint allows you to submit a payout by Bank Transfer in Peru.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" type="string" required="true" %}
Your App ID in payout platform.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" required="true" %}
Beneficiary's name, length must between 5 and 100
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" type="string" %}
Beneficiary's phone

\- 0 \~ 15 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
Beneficiary's email
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="bank_code" required="true" %}
Bank code, see [_**bank list**_](../../bank-code/bank-in-peru.md)_**​**_
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="account" required="true" %}
Account

\- 10 \~ 20 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="account_type" required="true" %}
Should be one of CHECKING, SAVINGS.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_id" type="string" required="true" %}
Beneficiary document id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_type" type="string" required="true" %}
Beneficiary document type, should be one of DNI, RUC, PAS, CE.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" required="true" %}
Fixed Value: BankTransfer
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" type="string" required="true" %}
Merchant's order id.&#x20;

\- Max.50 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" type="string" required="true" %}
One of \[beneficiary | merchant]
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="string" required="true" %}
Payout amount

\- Min 0.01, Max 500,000 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount_type" type="string" required="false" %}
Specify the amount value is fixed for merchant or beneficiary

\- One of: source\_amount, arrival\_amount(default) -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" type="string" required="true" %}
Merchant's account currency

\- supported: USD, GBP, EUR, PEN -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" type="string" required="true" %}
Beneficiary's account currency.

\- Fixed Value: PEN -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where pagsmile will callback to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additional_remark" type="string" required="true" %}
Additional Remark\
\- Max Length: 40 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" type="string" required="true" %}
Fixed value: PER, for Peru
{% endswagger-parameter %}

{% swagger-parameter in="body" name="region" type="string" required="true" %}
@See [_**Regions in Peru**_](regions-in-peru.md)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="success" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQBPE",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "100",
        "arrival_currency": "PEN",
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

{% swagger-response status="401: Unauthorized" description="unauthorized" %}
```javascript
{
    "code": 4004003,
    "msg": "permission denied",
    "time": 1637224716,
    "data": {}
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
      "phone" : "468****068",
      "email" : "g******me@gmail.com",
    * "bank_code": "0001", // Banco Continental
    * "account" : "00219400254640654321", // just for test in sandbox
    * "account_type" : "CHECKING",
    * "document_id" : "123456789", // just for test in sandbox, don't use this in production.
    * "document_type" : "PAS",
    * "method" : "BankTransfer",
    * "custom_code" : "custom_code9982674851738108",
    * "fee_bear" : "merchant",
    * "amount" : "100", 
    * "source_currency" : "PEN",
    * "arrival_currency" : "PEN",
    * "notify_url" : "https://notify.url",
    * "additional_remark" : "pagsmile payout test",
    * "country": "PER",
    * "region": "Amazonas"
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

## Example of Document

| Document Type | Document           | Description   |
| ------------- | ------------------ | ------------- |
| DNI           | 0\*\*\*\*\*\*6     | 8 digits      |
| RUC           | 1\*\*\*\*\*\*\*\*8 | 11 digits     |
| PAS           | 2\*\*\*\*\*\*\*\*9 | 9 - 16 digits |
| CE            | 3\*\*\*\*\*\*\*\*9 | 9 - 16 digits |

## Example of Account

| Bank                                    | Bank Code | Description                                                                       |
| --------------------------------------- | --------- | --------------------------------------------------------------------------------- |
| Banco Continental                       | 0001      | 18 or 20 digits                                                                   |
| Banco de Credito                        | 0002      | 13 digits for Current Account or Master Account and 14 digits for SAVINGS Account |
| Interbank                               | 0003      | 13 digits                                                                         |
| Scotiabank                              | 0004/0010 | 10 digits (3 agency + 7 account)                                                  |
| Any other bank or financial institution |           | 20-digit CCI interbank account code                                               |
