---
description: How to use BankTransfer to submit a payin in Bolivia.
---

# Bank Transfer

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/trade/pay" method="post" summary="Payin by BankTransfer" %}
{% swagger-description %}
This endpoint allows you to submit a payin by BankTransfer in Bolivia.
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
Fixed value: BOB
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="string" %}
payment amount\
\- 1 - 1,000,000 BOB -
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
User's bank account number\
\- numeric: 7 \~ 14 digits -&#x20;
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
\- CI: 7\~10 digits\
CE: 8 digits\
NIT: 9\~12 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" required="true" %}
User's identification type

\- CI, CE, NIT -
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
    "reference": "1102004201",
    "instruction":"{\"beneficiary\":{\"bank\":{\"code\":\"0039\",\"name\":\"BANCO GANADERO\",\"branch\":{\"code\":\"null\"},\"account\":{\"number\":\"1310825187\",\"type\":\"C\"}},\"document\":{\"id\":\"419326025\",\"type\":\"NIT\"},\"name\":\"Pagsmile\",\"type\":\"INDIVIDUAL\"},\"referenceCode\":\"1102004201\"}"
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

Format of customer.identify

<table><thead><tr><th width="146">Identify.type</th><th width="90">Length</th><th width="245">Format</th><th width="223">Description</th><th>Example</th></tr></thead><tbody><tr><td>CI</td><td>7-10</td><td>7 mandatory numerical digits and then optionally a space and two letters</td><td>Cedula de Identidad</td><td>SC 1234567 or 1234567</td></tr><tr><td>CE</td><td>8</td><td>numeric</td><td>Cedula de Identidad de Extranjero</td><td>12345678</td></tr><tr><td>NIT</td><td>9-12</td><td>numeric</td><td>Número de Identificación Tributaria</td><td>123456789</td></tr></tbody></table>

{% hint style="info" %}
The “CI” can be up to 10 characters. It is formed with 7 mandatory numerical digits and then optionally a space and two letters. The two letters represent the departments belonging to the “ Plurinational State of Bolivia”.

There are:

* BE - Beni
* CB- Cochabamba
* CH – Chuquisaca
* LP- La Paz
* OR- Oruro
* PD- Pando
* PT – Potosí
* SC – Santa Cruz
* TJ - Tarija

Examples : For Santa Cruz  you can send “SC 1234567”, “1234567”, “SC1234567”, “1234567SC” or “1234567 SC”
{% endhint %}

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
    * "order_currency": "BOB",
    * "subject": "trade pay test",
      "content": "trade pay test conent",
    * "notify_url": "http://merchant/callback/success",
      "return_url": "https://www.merchant.com",
    * "buyer_id": "buyer_0101_0001",
    * "timestamp": "2022-01-01 03:54:01",
      "timeout_express":"1c",
    * "bank":"004",
    * "account_number":"87654321",
    * "account_type":CHECKING",
    * "customer" : {
    *     "identify": {
    *         "type": "CI",
    *         "number": "12345678"
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
