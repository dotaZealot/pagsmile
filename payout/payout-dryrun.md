---
description: A simulation(dry run) for payout.
---

# Payout DryRun

{% swagger method="post" path="" baseUrl="https://sandbox.transfersmile.com/api/payout/dry-run" summary="A simulation(dry run) for payout." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" required="true" type="String" %}
application/json; chartset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" required="true" type="String" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Authorization" type="String" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" required="true" type="String" %}
Merchant's account currency

\- supported: USD, GBP, EUR -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" required="true" type="String" %}
BRL for BRA, MXN for MEX, USD for PayPal
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" required="true" type="String" %}
Numeric string, e.g. 10.00
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" required="true" type="String" %}
One of \[beneficiary, merchant]
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" required="true" type="String" %}
Payout Method
{% endswagger-parameter %}

{% swagger-parameter in="body" name="channel" type="String" %}
Payout Channel
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" required="true" type="String" %}
PayPal supported [countries](submit-a-payout/paypal/supported-countries.md).

Others must be one of \[BRA, MEX].
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" required="true" type="Integer" %}
unix timestamp, e.g. 1628512575
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1642076131,
    "data": {
        "fee": "0.2",
        "tax": "0",
        "amount": "10",
        "settlement_amount": "10",
        "arrival_currency": "USD",
        "arrival_amount": "10",
        "source_currency": "USD",
        "source_amount": "10.2",
        "exchange_rate": "1"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="" %}
```javascript
{
    "code": 4001000,
    "msg": "invalid parameter",
    "time": 1642078510,
    "data": {
        "err": "request has expired"
    }
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}
```javascript
{
    "code": 4004003,
    "msg": "permission denied",
    "time": 1642074682,
    "data": {}
}
```
{% endswagger-response %}
{% endswagger %}

## Example PIX

```
curl --location --request POST 'https://sandbox.transfersmile.com/api/payout/dry-run' \
--header 'AppId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
      * "source_currency": "USD",
      * "arrival_currency": "BRL",
      * "amount": "10.00",
      * "fee_bear": "merchant",
      * "method": "PIX",
        "channel": "",
      * "country": "BRA",
      * "timestamp": 1642075807
}'
```

## Example SPEI

```
curl --location --request POST 'https://sandbox.transfersmile.com/api/payout/dry-run' \
--header 'MerchantId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
      * "source_currency": "USD",
      * "arrival_currency": "MXN",
      * "amount": "10.00",
      * "fee_bear": "merchant",
      * "method": "SPEI",
        "channel": "",
      * "country": "MEX",
      * "timestamp": 1642075807
}'

```

## Example PayPal

```
curl --location --request POST 'https://sandbox.transfersmile.com/api/payout/dry-run' \
--header 'MerchantId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
      * "source_currency": "USD",
      * "arrival_currency": "USD",
      * "amount": "10.00",
      * "fee_bear": "merchant",
      * "method": "WALLET",
      * "channel": "PayPal",
      * "country": "BRA",
      * "timestamp": 1642075807
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is pagsmile's test merchant id for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}
