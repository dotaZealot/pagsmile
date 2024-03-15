---
description: How to use BankTransfer to submit a payin in Panama.
---

# Bank Transfer

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/trade/pay" method="post" summary="Payin by BankTransfer" %}
{% swagger-description %}
This endpoint allows you to submit a payin by BankTransfer in Panama.
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
Fixed value: USD
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="string" %}
payment amount\
\- 1 \~ 100,000 USD -
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

{% swagger-parameter in="body" name="bank" type="string" required="true" %}
Use [API](../../tools/supported-bank-list-query.md) to get bank code
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_number" type="string" %}
Account

\- 5 \~ 20 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_type" type="string" %}
Should be one of CHECKING, SAVINGS
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.name" type="string" required="true" %}
User's name
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.email" type="string" required="true" %}
User's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.number" type="string" required="true" %}
User's identification number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" required="true" %}
User's identification type

\- RUC, PASS or CE -
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
    "out_trade_no": "202201010354010",
    "web_url": "",
    "pay_url": "https://checkoutv2.pagsmile.com/checkout?prepay_id=",
    "trade_status": "PROCESSING",
    "reference":"ZRH9-FZAT-TAHV",
    "instruction":"{\"beneficiary\":{\"bank\":{\"code\":\"0079\",\"name\":\"LAFISE PANAMA\",\"branch\":[],\"account\":{\"number\":\"201020008603\",\"type\":\"C\"}},\"document\":{\"id\":\"155714930-2-2021\",\"type\":\"RUC\"},\"name\":\"LOCALPAYMENT PAN, S.A.\",\"type\":\"INDIVIDUAL\"},\"referenceCode\":\"ZRH9-FZAT-TAHV\"}",
    "due_date":"2024-02-14T09:00:15.993266"
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

**reference** is the ticket number that the user needs to use for payment
{% endhint %}

| Identify Type | Identify Number          | Description | Example                                                |
| ------------- | ------------------------ | ----------- | ------------------------------------------------------ |
| RUC           | Single Taxpayer Registry | 5-15 digits | 1790095389001                                          |
| PASS          | Passport                 | 5-20        | PD0404102                                              |
| CE            | Cedula (Local ID)        | 5-12        | <p>8-211-1816</p><p>E-1234-12345<br>1AV-1234-12345</p> |

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "out_trade_no": "202201010354010",
    * "method": "BankTransfer",
    * "order_amount": "12.01",
    * "order_currency": "USD",
    * "subject": "trade pay test",
      "content": "trade pay test conent",
    * "notify_url": "http://merchant/callback/success",
      "return_url": "https://www.merchant.com",
    * "buyer_id": "buyer_0101_0001",
    * "timestamp": "2022-01-01 03:54:01",
      "timeout_express":"1c",
    * "bank": "1805",
    * "account_number": "12**4324",
    * "account_type": "C",
    * "customer": {
    *     "identify": {
    *        "type": "RUC",
             "number": "390**7"
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

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption><p>Example of Panama Payment page</p></figcaption></figure>
