---
description: How to use BNCR to submit a payin in Costa Rica.
---

# BNCR

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/trade/pay" method="post" summary="Payin by BNCR" %}
{% swagger-description %}
This endpoint allows you to submit a payin by BNCR in Costa Rica.
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
Fixed value: BNCR
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_currency" required="true" type="string" %}
Fixed value: CRC
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="string" %}
payment amount\
\- 1000\~600,000 CRC\
(only integer) -
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

{% swagger-parameter in="body" name="customer.name" type="string" required="true" %}
User's name
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.phone" type="string" required="true" %}
User's phone
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.email" type="string" required="true" %}
User's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.number" type="string" required="false" %}
User's identification number\
\- 9 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" required="false" %}
User's identification type

\- CDI -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.zip_code" required="false" type="string" %}
zip code\
\- 5 digits -
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
    "trade_no": "2022010106532400030",
    "out_trade_no": "202201010354009",
    "web_url": "",
    "pay_url":"https://checkout.pagsmile.com/checkout?prepay_id=",
    "trade_status": "PROCESSING",
    "reference": "90985633144",
    "partner_code":"" //The partner_code could be different
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

{% hint style="info" %}
**User payment tips**

* A BNCR order can be paid through e-banking or at Branches and Agencies.
* The maximum amount per transaction through **BNCR e-banking** is **CRC ₡ 600,000.00**. The maximum amount per transaction at BNCR at **Branches** and **Agencies** is **CRC ₡ 190,000.00**
{% endhint %}

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "162************38",
    "out_trade_no": "202201010354009",
    "method": "BNCR",
    "order_amount": "1000",
    "order_currency": "CRC",
    "subject": "trade pay test",
    "content": "trade pay test conent",
    "notify_url": "http://merchant/callback/success",
    "return_url": "https://www.merchant.com",
    "buyer_id": "buyer_0101_0001",
    "timestamp": "2022-01-01 03:54:01",
    "timeout_express":"1c",
    "customer" : {
        "identify": {
            "type": "CDI",
            "number": "502844147"
        },
        "name": "Test User Name",
        "email": "test@pagsmile.com",
        "phone": "50687898788"
    },
    "address" : {
        "zip_code": "01130",
    }'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
