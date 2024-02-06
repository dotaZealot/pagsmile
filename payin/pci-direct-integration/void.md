---
description: How to void an authorization.
---

# Void

{% hint style="info" %}
An authorization can be voided before it is captured if the payment is no longer needed.
{% endhint %}

{% swagger method="post" path="/trade/void" baseUrl="https://gateway-test.pagsmile.com" summary="Void Authorization" %}
{% swagger-description %}
This endpoint allows you to void an authorization.
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

{% swagger-parameter in="body" type="string" name="out_trade_no" required="true" %}
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

{% swagger-response status="400: Bad Request" description="failed" %}
```json
{
    "msg": "Business Failed",
    "code": "40002"
}
```
{% endswagger-response %}
{% endswagger %}

### Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/void' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "1617****052",
    "timestamp": "2022-08-11 16:17:36",
    "version": "2.0",
    "out_trade_no": "836***93"
}'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
