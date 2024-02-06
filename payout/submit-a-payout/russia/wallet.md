---
description: Where to submit a payout by Wallet in Russia.
---

# Wallet

{% swagger method="post" path="api/payout" baseUrl="https://sandbox.transfersmile.com/" summary=" Submit a payout by Wallet in Russia" %}
{% swagger-description %}
This endpoint allows you to submit a payout by e-Wallet in Russia.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" required="true" type="String" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" required="true" type="String" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" required="true" type="String" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String" %}
Beneficiary's name

\- Min.5 Max.100 -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="phone" %}
Beneficiary's phone.

\- 0 \~ 15 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="email" %}
Beneficiary's email

\- Max.64 -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="account" required="true" %}
Beneficiary Qiwi account.

\- 11 \~ 12 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="account_type" required="true" %}
Fixed Value: PHONE
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="method" required="true" %}
Fixed Value: WALLET
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="channel" required="true" %}
Fixed Value: Qiwi
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" type="String" required="true" %}
Merchant's order id

\- Max. 50 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" type="String" required="true" %}
Processing fee charges to merchant or beneficiary.\
\- One of: merchant beneficiary -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="String" required="true" %}
Payout Amount, 2 decimal numbers

\- Min 1, Max 250,000 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount_type" type="String" %}
Specify the amount value is fixed for merchant or beneficiary\
\- One of: source\_amount, arrival\_amount(default) -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" type="String" required="true" %}
Merchant Account Currency\
\- One of: USD, EUR, GBP -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" type="String" required="true" %}
Fixed value: RUB
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="String" required="true" %}
Where pagsmile will send notification to.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additional_remark" type="String" required="true" %}
Descriptor on the user's bank bill\
\- Max length: 40 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" type="String" required="true" %}
Fixed Value: RUS for Russia
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="successfully" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQM",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "0.51",
        "arrival_currency": "RUB",
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
    "data": {}
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
      "name": "GUILHERME ****** SOUZA",
      "phone": "468****068",
      "email": "g******me@gmail.com",
    * "account": "7317*****412",
    * "account_type": "PHONE", // Fixed Value: PHONE
    * "method": "WALLET", // Fixed Value: WALLET
    * "channel": "Qiwi",  // Fixed Value: Qiwi
    * "custom_code": "custom_code9982674851738108", // merchant order id
    * "fee_bear": "merchant",
    * "amount": "100", 
    * "source_currency": "USD",
    * "arrival_currency": "RUB",
    * "notify_url": "https://notify.url",
    * "additional_remark": "pagsmile payout test",
    * "country": "RUS"
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

{% hint style="success" %}
In **sandbox** environment, please use _<mark style="color:red;">**79991112244**</mark>_ as  <mark style="color:blue;">**Qiwi**</mark> account for testing **Failed** payout, any other <mark style="color:blue;">**Qiwi**</mark> account will be successful.
{% endhint %}

## Account

| Account Type | Account      | Description  |
| ------------ | ------------ | ------------ |
| PHONE        | 712345678901 | 11-12 digits |
