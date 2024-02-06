---
description: How to use BankTransfer to submit a payin in Paraguay.
---

# ❌ Bank Transfer

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/trade/pay" method="post" summary="Payin by BankTransfer" %}
{% swagger-description %}
This endpoint allows you to submit a payin by BankTransfer in Paraguay.
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
Fixed value: BankTransfer
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_currency" required="true" type="string" %}
Fixed value: PYG
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="string" %}
payment amount\
\- 1 - 5,000,000 PYG -
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

{% swagger-parameter in="body" name="bank" required="true" type="string" %}
Use [API](../../tools/supported-bank-list-query.md) to get bank code
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_number" required="true" type="string" %}
User's bank account number
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="account_type" required="true" %}
User's bank account type

\- One of: SAVINGS, CHECKING -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.name" type="string" required="true" %}
User's name
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.phone" type="string" required="false" %}
User's phone
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.email" type="string" required="true" %}
User's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.number" type="string" required="true" %}
User's identification number\
\- CI: 7 digits&#x20;

&#x20;  RUC: 8-9 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" required="true" %}
User's identification type

\- CI, RUC -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.zip_code" required="false" type="string" %}
zip code\
\- 5 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.state" type="string" %}
state
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.city" type="string" %}
city
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.street_number" type="string" %}
street number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.street" type="string" %}
street
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
    "out_trade_no": "202201010354008",
    "web_url": "",
    "pay_url":"https://checkout-test.pagsmile.com/checkout?prepay_id=",
    "trade_status": "PROCESSING",
    "reference": "2901004200",
    "instruction":"{\"beneficiary\":{\"bank\":{\"code\":\"0040\",\"name\":\"BANCO ITAU PARAGUAY S.A.\",\"branch\":{\"code\":\"null\"},\"account\":{\"number\":\"215559\",\"type\":\"C\"}},\"document\":{\"id\":\"80121508-0\",\"type\":\"RUC\"},\"name\":\"Pagsmile\",\"type\":\"INDIVIDUAL\"},\"referenceCode\":\"2901004200\"}"
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

* Take the recipient's bank details from the response parameter - "instruction" and present to users
{% endhint %}

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "out_trade_no": "202201010354008",
    * "method": "BankTransfer",
    * "order_amount": "50",
    * "order_currency": "PYG",
    * "subject": "trade pay test",
      "content": "trade pay test conent",
    * "notify_url": "http://merchant/callback/success",
      "return_url": "https://www.merchant.com",
    * "buyer_id": "buyer_0101_0001",
    * "timestamp": "2022-01-01 03:54:01",
      "timeout_express":"1c",
    * "bank":"015",
    * "account_number":"678901",
    * "account_type":CHECKING",
    * "customer" : {
    * "identify": {
    *         "type": "CI",
    *         "number": "1234567"
      },
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
