---
description: How to get your account balance in Pagsmile.
---

# Account Balance

{% swagger method="post" path="" baseUrl="https://sandbox.transfersmile.com/api/balance" summary="Get your account balance in pagsmile." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" required="true" type="String" %}
application/json; chartset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="AppId" type="String" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Authorization" type="String" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" required="true" type="Integer" %}
unix timestamp, e.g. 1628512575
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1642075813,
    "data": [
        {
            "currency": "USD",
            "amount": "551.38"
        },
        {
            "currency": "GBP",
            "amount": "0"
        },
        {
            "currency": "EUR",
            "amount": "0"
        },
        {
            "currency": "BRL",
            "amount": "99002.23"
        },
        {
            "currency": "MXN",
            "amount": "0"
        }
    ]
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

## Example

```
curl --location --request POST 'https://sandbox.transfersmile.com/api/balance' \
--header 'AppId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
   * "timestamp": 1642075807
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is pagsmile's test merchant id for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID
{% endhint %}
