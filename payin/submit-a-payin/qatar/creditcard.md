---
description: How to use CreditCard to submit a payin in Qatar.
---

# Credit Card

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/trade/pay" method="post" summary="Payin by CreditCard" %}
{% swagger-description %}
This endpoint allows you to submit a payin by CreditCard in Qatar.
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

{% swagger-parameter in="body" name="out_trade_no" type="string" required="true" %}
ID given by the merchant in their system\
\- Max. 64 chars -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" required="true" %}
Fixed value: CreditCard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_currency" required="true" type="string" %}
Fixed value: QAR
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="string" %}
payment amount\
\- 0.5\~50000 QAR -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="subject" required="true" type="string" %}
payment reason or item title

\- Max. 128 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" type="string" %}
payment reason detail or item detail

\- Max. 255 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where Pagsmile will send notification to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="return_url" type="string" %}
Redirect to Merchant's url when user finished checkout
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_id" required="true" type="string" %}
merchant user's id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user_ip" required="true" type="string" %}
user's IP address
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" required="true" type="string" %}
use [Pagsmile Javascript](../../tools/pagsmile-javascript.md) to get toekn
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fingerprint" required="true" type="string" %}
use [Pagsmile Javascript](../../tools/pagsmile-javascript.md) to get fingerprint
{% endswagger-parameter %}

{% swagger-parameter in="body" name="issuer" required="true" type="string" %}
issuer of CreditCard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="installments" type="string" %}
installments for CreditCard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.name" type="string" required="true" %}
User's name
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.phone" type="string" required="true" %}
User's phone
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.email" type="string" required="true" %}
User's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" required="true" %}
User's identification type
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify" type="string" required="true" %}
User's identification number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.zip_code" required="true" type="string" %}
zip code
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.state" type="string" %}
state\
\- Required if zip\_code not provide -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.city" type="string" %}
city

\- Required if zip\_code not provide -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.street_number" type="string" %}
street number

\- Required if zip\_code not provide -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.street" type="string" %}
street

\- Required if zip\_code not provide -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="website_url" type="string" %}
merchant website URL

\- Max. 128 chars -
{% endswagger-parameter %}

{% swagger-response status="200" description="submit successfully" %}
```
{
    "code": "10000",
    "msg": "Success",
    "trade_no": "2022010110293900084",
    "out_trade_no": "202201010354003",
    "web_url": "",
    "trade_status": "PROCESSING"
}
```
{% endswagger-response %}

{% swagger-response status="400" description="duplicate out_trade_no" %}
```
{
    "code": "40002",
    "msg": "Business Failed",
    "sub_code": "duplicate-out_trade_no",
    "sub_msg": "out_trade_no is duplicate"
}
```
{% endswagger-response %}
{% endswagger %}

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "162************38",
    "out_trade_no": "202201010354003",
    "method": "CreditCard",
    "order_amount": "100.00",
    "order_currency": "QAR",
    "subject": "trade pay test",
    "content": "trade pay test conent",
    "notify_url": "http://merchant/callback/success",
    "return_url": "https://www.merchant.com",
    "buyer_id": "buyer_0101_0001",
    "user_ip":"127.0.0.1",
    "token":"${token}",
    "fingerprint":"${fingerprint}",
    "issuer":"visa",
    "timestamp": "2022-01-01 03:54:01",
    "timeout_express":"1c",
    "customer" : {
        "name": "Test User Name",
        "email": "test@pagsmile.com",
        "phone": "75991435892"
    },
    "address" : {
        "zip_code": "38082365",
    }'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
