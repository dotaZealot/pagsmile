---
description: How to use BankTransfer to submit a payin in Argentina.
---

# ❌ Bank Transfer

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/trade/pay" method="post" summary="Payin by BankTransfer " %}
{% swagger-description %}
This endpoint allows you to submit a payin by BankTransfer in Argentina.
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
Fixed value: ARS
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="string" %}
payment amount\
\- 1\~1,000,000 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="subject" required="true" type="string" %}
payment reason or item title

\- Max. 128 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" type="string" required="true" %}
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

{% swagger-parameter in="body" name="bank" type="string" required="true" %}
Please use the [API](../../tools/supported-bank-list-query.md) to get supported bank list
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_type" type="string" required="true" %}
bank account type\
\- C (Checking account) or S (Savings account) -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_number" type="string" required="true" %}
Max 22 digits
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
\- 11 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" required="true" %}
User's identification type

\- CUIT/CUIL/CDI -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.zip_code" required="false" type="string" %}
zip code\
\- 6 digits -
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
    "code":"10000",
    "msg":"Success",
    "prepay_id":"d3UwdDhRbnUx****NMzdaWT0=-17FBDFe8",
    "trade_no":"2022010110293900083",
    "out_trade_no":"202201010354006",
    "web_url":"",
    "pay_url":"https://checkout.pagsmile.com/checkout?prepay_id=",
    "trade_status":"PROCESSING",
    "reference":"1024001122",
    "instruction":"{\"beneficiary\":{\"bank\":{\"code\":\"0002\",\"name\":\"ICBC\",\"branch\":{\"code\":\"null\"},\"account\":{\"number\":\"0150**************3082\",\"type\":\"Checking\"}},\"document\":{\"id\":\"30716132028\",\"type\":\"CUIT\"},\"name\":\"Test\",\"type\":\"INDIVIDUAL\"},\"referenceCode\":\"1024001122\"}"
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

* Redirect users to the **pay\_url** to complete the payment
* the first three digits of the account number must be the same as the bank code. For example, if the bank code is 191, the account number must be 191xxxxxxxxxxxxxxxxxxx.
{% endhint %}

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "out_trade_no": "202201010354006",
    * "method": "BankTransfer",
    * "order_amount": "50",
    * "order_currency": "ARS",
    * "subject": "trade pay test",
    * "content": "trade pay test conent",
    * "notify_url": "http://merchant/callback/success",
      "return_url": "https://www.merchant.com",
    * "buyer_id": "buyer_0101_0001",
    * "timestamp": "2022-01-01 03:54:01",
      "timeout_express":"1c",
    * "account_number": "1910**************6653",
    * "account_type": "C",
    * "bank":"191",
    * "customer" : {
    *     "identify": {
    *         "type": "CUIT",
    *         "number": "20115872045"
          },
    *     "name": "Test User Name",
    *     "email": "test@pagsmile.com"
      }
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
