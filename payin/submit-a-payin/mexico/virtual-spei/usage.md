---
description: How to check usage of virtual SPEI account.
---

# Check Usage of Virtual SPEI Account

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/virtual-account/spei/usage" method="post" summary="Payin by SPEI" %}
{% swagger-description %}
This endpoint allows you to check usage of virtual SPEI account.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; chartset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic Base($app\__id:$security\__key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="app_id" type="string" required="true" %}
created app's id at dashboard

\- Max. 32 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" required="true" type="string" %}
yyyy-MM-dd HH:mm:ss\
\- Max. 19 chars -
{% endswagger-parameter %}

{% swagger-response status="200" description="submit successfully" %}
```
{
    "used": 2000,
    "unused": 1000
}
```
{% endswagger-response %}

{% swagger-response status="400" description="account pool run out" %}
<pre><code>{
<strong>    "code": "40002",
</strong>    "msg": "Business Failed",
    "sub_code": "account-pool-run-out",
    "sub_msg": "account pool run out"
}
</code></pre>
{% endswagger-response %}
{% endswagger %}

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/virtual-account/spei/usage' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "timestamp": "2022-01-01 03:54:01"
      }'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
