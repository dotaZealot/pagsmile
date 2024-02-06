---
description: How to use Bank Transfer to submit a payout in Uruguay.
---

# BankTransfer

{% swagger method="post" path="/api/payout" baseUrl="https://sandbox.transfersmile.com" summary="Submit a payout by Bank Transfer in Uruguay." %}
{% swagger-description %}
This endpoint allows you to submit a payout by Bank Transfer in Uruguay.
{% endswagger-description %}

{% swagger-parameter in="body" name="name" type="String" required="true" %}
Beneficiary's name\
\- Length must between 5 and 100 -
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Content-Type" type="String" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="phone" required="true" %}
Beneficiary's phone

\- 0 \~ 15 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="email" required="true" %}
Beneficiary's email
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" type="String" name="AppId" %}
Your App ID in payout platform.
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="document_id" required="true" %}
Beneficiary's identification number.
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" type="String" name="Authorization" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="document_type" required="true" %}
Beneficiary's identification type.

\- One of: CI, RUT -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="bank_code" required="true" %}
Bank Code in Uruguay, see [_**bank list**_](../../bank-code/bank-in-uruguay.md)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" type="String" required="true" %}
Beneficiary's Bank Account

\- 2 \~ 14 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_type" type="String" required="true" %}
Beneficiary's Account Type

\- One of: SAVINGS, CHEKCING -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="String" required="true" %}
Fixed value: BANKTRANSFER
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="custom_code" required="true" %}
Merchant Payout ID

\- Max. 50 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" type="String" required="true" %}
Processing fee charges to merchant or beneficiary

\- One of: merchant, beneficiary -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="String" required="true" %}
Payout Amount, 2 decimal numbers

\- Min 1, Max 5,000,000 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount_type" type="String" %}
Specify the amount value is fixed for merchant or beneficiary

\- One of: source\_amount, arrival\_amount(default) -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" type="String" required="true" %}
Merchant Account Currency

\- One of: USD, EUR, GBP -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" type="String" required="true" %}
Fixed value: UYU
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="String" required="true" %}
Where pagsmile will send notifications to.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additional_remark" type="String" required="true" %}
The descriptor on the user's bank bill

\- Max. 40 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" type="String" required="true" %}
Fix value: URY, for Uruguay
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="submit successfully" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQM",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "0.51",
        "arrival_currency": "UYU",
        "source_amount": "0.07",
        "source_currency": "USD",
        "status": "IN_PROCESSING"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="order already existed" %}
```javascript
{
    "code": 4001010,
    "msg": "order already existed",
    "time": 1628580940,
    "data": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="unauthorized" %}
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
        ... ...
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
    * "phone": "12******9",
    * "email": "payout@pagsmile.com",
    * "bank_code": "1001",
    * "account_type": "CHECKING", // should be one of SAVINGS, CHECKING
    * "account": "6***8",
    * "document_id": "12*******91",
    * "document_type": "CI",  // should be one of CI, RUT
    * "source_currency": "USD", 
    * "arrival_currency": "UYU", // fixed value: UYU
    * "fee_bear": "merchant", // should be one of merchant, beneficiary
    * "method": "BANKTRANSFER", // fixed value: BANKTRANSFER
    * "amount": "1.80",
    * "notify_url": "https://notify.url",
    * "custom_code" : "custom_code9982674851738108",
    * "additional_remark": "pagsmile payout test remark",
    * "country": "URY"  // fixed value: URY
}
'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is the authorization token associated with the test App ID.
{% endhint %}

## Example of Document

| Document Type | Document               | Description |
| ------------- | ---------------------- | ----------- |
| CI            | 0\*\*\*\*\*\*6         | 8 digits    |
| RUT           | 2\*\*\*\*\*\*\*\*\*\*8 | 12 digits   |

## Example of Account

| Bank          | Bank Code | Description  |
| ------------- | --------- | ------------ |
| BROU          | 1001      | 14 digits    |
| BHU           | 1091      | 10 digits    |
| BANDES        | 1110      | 9 digits     |
| ITAU          | 1113      | 7 digits     |
| SCOTIABANK    | 1128      | 10 digits    |
| SANTANDER     | 1137      | 12 digits    |
| BBVA          | 1153      | 2 - 9 digits |
| HSBC          | 1157      | 10 digits    |
| HERITAGE      | 1162      | 9 digits     |
| CITIBANK      | 1205      | 10 digits    |
| NACION        | 1246      | 12 digits    |
| BAPRO         | 1361      | 7 digits     |
| PREX (FORTEX) | 7905      | 8 digits     |
