---
description: How to use Wallet to submit a payout in Argentina.
---

# Wallet

{% swagger method="post" path="/api/payout" baseUrl="https://sandbox.transfersmile.com" summary="Submit a payout by Wallet in Argentina." %}
{% swagger-description %}
This endpoint allows you to submit a payout by Wallet in Argentina.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String" required="true" %}
Beneficiary's name\
\- Length must between 5 and 100 -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="phone" %}
Beneficiary's phone&#x20;

\- 0 \~ 15 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="email" %}
Beneficiary's email
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="document_id" required="true" %}
Beneficiary's identification number.
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="document_type" required="true" %}
Beneficiary's identification type.

Fixed value: CUIT
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" type="String" required="true" %}
Beneficiary's  Account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_type" type="String" required="true" %}
Beneficiary's Account Type

\- Fixed value: CVU -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="String" required="true" %}
Fixed value: WALLET
{% endswagger-parameter %}

{% swagger-parameter in="body" name="channel" type="String" required="true" %}
Fixed value: MercadoPago
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" type="String" required="true" %}
Merchant Payout ID

\- Max. 50 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" type="String" required="true" %}
Processing fee charges to merchant or beneficiary

\- One of: merchant, beneficiary -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="amount" required="true" %}
Payout Amount, 2 decimal numbers

\- Min 1, Max 10,000,000 -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="amount_type" %}
Specify the amount value is fixed for merchant or beneficiary

\- One of: source\_amount, arrival\_amount(default) -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" required="true" type="String" %}
Merchant Account Currency

\- One of: USD, EUR, GBP, ARS -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" required="true" type="String" %}
Fixed value: ARS
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" required="true" type="String" %}
Where pagsmile will send notifications to.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" type="String" required="true" %}
Your App ID in payout platform.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additional_remark" required="true" type="String" %}
The descriptor on the user's bank bill

\- Max. 40 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" required="true" type="String" %}
Fix value: ARG, for Argentina
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="submit successfully" %}
```json
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQM",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "0.51",
        "arrival_currency": "ARS",
        "source_amount": "0.07",
        "source_currency": "USD",
        "status": "IN_PROCESSING"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="order already existed" %}
```json
{
    "code": 4001010,
    "msg": "order already existed",
    "time": 1628580940,
    "data": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="permission denied" %}
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
      "phone": "12******9",
      "email": "payout@pagsmile.com",
    * "account_type": "CVU", // fixed value: CVU
    * "account": "00000031************56",
    * "document_id": "12*******91",
    * "document_type": "CUIT",  // fixed value: CUIT
    * "source_currency": "USD", 
    * "arrival_currency": "ARS", // fixed value: ARS
    * "fee_bear": "merchant", // should be one of merchant, beneficiary
    * "method": "WALLET", // fixed value: WALLET
    * "channel": "MercadoPago", // fixed value: MercadoPago
    * "amount": "1.80",
    * "notify_url": "https://notify.url",
    * "custom_code" : "merchant_payout_order_id",
    * "additional_remark": "pagsmile payout test remark",
    * "country": "ARG"  // fixed value: ARG
}
'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is the authorization token associated with the test App ID.
{% endhint %}

## Example of Document

| Document Type | Document ID        | Description |
| ------------- | ------------------ | ----------- |
| CUIT          | 27\*\*\*\*\*\*\*00 | 11 digits   |

## Example of Account

| Account Type | Account                            | Description                                       |
| ------------ | ---------------------------------- | ------------------------------------------------- |
| CVU          | 00000031\*\*\*\*\*\*\*\*\*\*\*\*56 | Always start with  00000031, should be 22 digits. |
