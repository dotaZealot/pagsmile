---
description: How to use PayPal to submit a payout.
---

# PayPal



{% swagger method="post" path="" baseUrl="https://sandbox.transfersmile.com/api/payout" summary="Submit a payout by PayPal globally." %}
{% swagger-description %}
This endpoint allows you to submit a payout by PayPal globally.
{% endswagger-description %}

{% swagger-parameter in="header" required="true" name="Content-Type" type="string" %}
application/json; chartset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="AppId" type="String" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Authorization" type="String" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" required="false" type="String" %}
Beneficiary's name

\- Min.5 Max.100 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" type="String" %}
Beneficiary's phone.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="String" %}
Beneficiary's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" required="true" type="String" %}
PayPal account.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_type" required="true" type="String" %}
Fixed: EMAIL
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_id" required="false" type="String" %}
Beneficiary document id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_type" required="false" type="String" %}
Beneficiary document type
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" required="true" type="String" %}
Fixed: WALLET
{% endswagger-parameter %}

{% swagger-parameter in="body" name="channel" required="true" type="String" %}
Fixed: PayPal
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" required="true" type="String" %}
Merchant's order id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" required="true" type="String" %}
One of \[beneficiary | merchant]&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" required="true" type="String" %}
Payout Amount, 2 decimal numbers

\- Min 0.01, Max 50,000 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="amount_type" %}
Specify the amount value is fixed for merchant or beneficiary\
\- One of: source\_amount, arrival\_amount(default) -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" required="true" type="String" %}
Merchant's account currency

\- supported: USD, GBP, EUR -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" required="true" type="String" %}
Beneficiary's account currency.

@See [supported currencies](supported-countries.md)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" required="true" type="String" %}
Where pagsmile will callback to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additional_remark" required="true" type="String" %}
Payout Remark

\- Max length: 40 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" type="String" required="true" %}
Beneficiary's Country/Region code.

@See [supported countries](supported-countries.md)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="submit successfully" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQPB",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "0.51",
        "arrival_currency": "BRL",
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
    "data": {
        ... ...
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
 // balance insufficient
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

{% swagger-response status="500: Internal Server Error" description="server error" %}
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
      "name" : "GUILHERME ****** SOUZA",
      "phone" : "468****068",
      "email" : "g******me@gmail.com",
    * "account" : "paid@pagsmile.com",
    * "account_type" : "EMAIL",
      "document_id" : "**********",
      "document_type" : "***",
    * "method" : "WALLET",
    * "channel" : "PayPal",
    * "custom_code" : "custom_code_your_order_id",
    * "fee_bear" : "merchant",
    * "amount" : "0.51",
    * "source_currency" : "USD",
    * "arrival_currency" : "USD",
    * "notify_url" : "https://your.notify.url",
    * "additional_remark" : "pagsmile payout test",
    * "country": "USA"
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

{% hint style="success" %}
In sandbox environment, please use _<mark style="color:green;">**`paid@pagsmile.com`**</mark>_ as  <mark style="color:blue;">**PayPal**</mark> account for testing success payout, any other <mark style="color:blue;">**PayPal**</mark> account will be failed.
{% endhint %}
