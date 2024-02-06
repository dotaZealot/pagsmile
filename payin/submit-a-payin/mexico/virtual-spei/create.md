---
description: How to create virtual SPEI account to submit a payin in Mexico.
---

# Create Virtual SPEI Account

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/virtual-account/spei/create" method="post" summary="Payin by SPEI" %}
{% swagger-description %}
This endpoint allows you to create virtual SPEI account number in Mexico.
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

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where Pagsmile will send notification to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.buyer_id" type="string" required="true" %}
Customer's user id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.name" type="string" required="true" %}
User's name
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.email" type="string" required="true" %}
User's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.number" type="string" required="true" %}
User's identification number\
\- 13 chars, ex: MAMB780915969; CURP: 18 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" required="true" %}
User's identification type

\- RFC  or CURP -
{% endswagger-parameter %}

{% swagger-response status="200" description="submit successfully" %}
<pre><code>{
<strong>    "account_id": "692W********MRW4",
</strong>    "account_number": "6461xxxxxxxxxx0137", //Clabe
    "buyer_id": "0001",
    "provider": "STP", //Bank name
    "status": "ACTIVE", //Status ENUM[ACTIVE/CANCELED]
    "beneficiary_name": "PAGSMILE MEXICO SA DE CV",
    "notify_url": "https://your-notify-url.com"
}
</code></pre>
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
curl --location --request POST 'https://gateway-test.pagsmile.com/virtual-account/spei/create' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "notify_url": "http://merchant/callback/success",
    * "timestamp": "2022-01-01 03:54:01",
    * "customer" : {
    *     "identify": {
    *         "type": "RFC",
    *         "number": "MAMB780915969"
          },
    *     "buyer_id": "buyer_0101_0001",
    *     "name": "Test User Name",
    *     "email": "test@pagsmile.com"
      }
      }'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
