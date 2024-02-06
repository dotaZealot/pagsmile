---
description: How to request a checkout page.
---

# Checkout Page

{% swagger method="post" path="/api/checkout" baseUrl="https://sandbox.transfersmile.com " summary="This endpoint allows you to request a checkout page." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" required="true" type="String" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" required="true" type="String" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Authorization" type="String" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user_id" required="true" type="String" %}
user id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" required="true" type="String" %}
merchant payout id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" required="true" type="String" %}
one of \[beneficiary | merchant]&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="String" %}
Payment Method

\- e.g. PIX, SPEI, PayPal,BANKTRANSFER -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" required="true" type="String" %}
Merchant Account Currency

\- One of: USD, EUR, GBP, BRL -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="payout_currency" required="true" type="String" %}
Payout/Arrival Currency

\- One of: USD, BRL, MXN -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="payout_amount" required="true" type="String" %}
Payout Amount, Numeric&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timeout" type="Integer" %}
default & max 1800 seconds
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" required="true" type="String" %}
Where pagsmile will send notification to.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="return_url" required="true" type="String" %}
When a user completes the payout, where will return back to.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additional_remark" required="true" type="String" %}
transaction description

\- Length must less than 40 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" type="String" %}
BRA for Brazil

MEX for Mexico

GLOBAL for PayPal
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1639473556,
    "data": {
        "checkout_url": "https://sandbox-payout.pagsmile.com/?t=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjoiMTAwMDEiLCJwYXlvdXRfaWQiOiJUUzIwMjExMjE0MDkxOTE2NHExNE4yVUhCVTVYQiIsImN1c3RvbV9jb2RlIjoiY2hlY2tvdXRfdGVzdF8xMDAwMDQiLCJmZWVfYmVhciI6Im1lcmNoYW50Iiwic291cmNlX2N1cnJlbmN5IjoiVVNEIiwicGF5b3V0X2N1cnJlbmN5IjoiVVNEIiwicGF5b3V0X2Ftb3VudCI6IjEwLjAxIiwibm90aWZ5X3VybCI6Imh0dHBzOi8vc2FuZGJveC50cmFuc2ZlcnNtaWxlLmNvbS9hcGkvbm90aWZ5L2RlbW8iLCJyZXR1cm5fdXJsIjoiaHR0cHM6Ly93d3cuYmFpZHUuY29tIiwiYWRkaXRpb25hbF9yZW1hcmsiOiJjaGVja291dCB0ZXN0IiwiY291bnRyeSI6IkJSQSIsInNlc3Npb25fdGltZW91dCI6MTgwMCwiY3JlYXRlZF9hdCI6MTYzOTQ3MzU1NiwiaXNzIjoiUGFnc21pbGUgLSBUcmFuc2ZlcnNtaWxlIiwiZXhwIjoxNjM5NDc1MzU2LCJqdGkiOiIzMiJ9.6Bmm2jrJUtlfWy9FrxPagsmilePayouttIwbhUx-OoCdU2aZMw"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="" %}
```javascript
{
    "code": 4001000,
    "msg": "invalid parameter",
    "time": 1637224716,
    "data": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}
```javascript
{
    "code": 4004003,
    "msg": "permission denied",
    "time": 1638154829,
    "data": {}
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}
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

## Request Example

```
curl --location --request POST 'https://sandbox.transfersmile.com/api/checkout' \
--header 'AppId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
    "user_id": "10001",
    "custom_code": "my_checkout_test_10001",
    "source_currency": "USD",
    "payout_currency": "BRL",
    "fee_bear": "merchant",
    "payout_amount": "10.01",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "return_url": "https://merchant.return.url",
    "additional_remark": "pagsmile checkout test",
    "country": "BRA"
}'   
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is pagsmile's test merchant id for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

## Checkout Logo

| Front End | Specification |
| --------- | ------------- |
| WEB       | 128px \* 64px |
| H5        | 42px \* 42px  |

## Supported Countries

| Country Code | Payment Method    | Source Currency | Payout Currency |
| ------------ | ----------------- | --------------- | --------------- |
| BRA(Brazil)  | PIX, Banktransfer | USD, BRL        | BRL             |
| MEX(Mexico)  | SPEI              | USD, MXN        | MXN             |
| GLOBAL       | PayPal            | USD             | USD             |

{% hint style="info" %}

{% endhint %}
