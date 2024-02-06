---
description: How to capture an authorization.
---

# Capture

{% swagger method="post" path="/trade/capture" baseUrl="https://gateway-test.pagsmile.com" summary="Capture Authorization" %}
{% swagger-description %}
This endpoint allows you to capture an authorization.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; chartset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="app_id" required="true" %}
created app's id at dashboard

\- Max. 32 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" type="string" required="true" %}
yyyy-MM-dd HH:mm:ss\
\- Max. 19 chars -
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Authorization" type="string" %}
Basic Base($app\__id:$security\__key)
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="version" required="false" %}
fixed value: 2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="amount" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" required="true" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="out_trade_no" required="true" type="string" %}
ID given by the merchant in their system\
\- Max. 64 chars -&#x20;
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="submit successfully" %}
```json
{
    "msg": "Success",
    "code": "10000"
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="invalid signature" %}
```json
{
    "code":"40002",
    "msg":"Business Failed",
    "sub_code":"invalid-signature",
    "sub_msg":"invalid signature"
}
```
{% endswagger-response %}
{% endswagger %}

### Example

```
curl --location --request POST 'https://security-test.pagsmile.com/card/token' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "1617***052",
    "timestamp": "2022-08-11 10:26:03",
    "version": "2.0",
    "amount": "90",
    "currency": "brl",
    "out_trade_no": "out_18***1300"
}'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
