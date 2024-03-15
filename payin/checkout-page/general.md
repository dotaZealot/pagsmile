---
description: How to use Pagsmile Checkoutpage to submit a payin.
---

# Checkout Page (General)

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/trade/create" method="post" summary="Payin by using Pagsmile checkout page" %}
{% swagger-description %}
This endpoint allows you to submit a payin by using Pagsmile checkout page
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

{% swagger-parameter in="body" name="method" type="string" required="false" %}
Add this object to show only the selected method. For instance, “method”: “PIX” will only show the PIX method. To show all the methods do not add this object in the request body. Check [here](../data/payment-method.md) for all methods
{% endswagger-parameter %}

{% swagger-parameter in="body" name="channel" type="string" %}
only use when method = Wallet
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_currency" required="true" type="string" %}
order currency\
\- Max. 3 chars -\
Check [here](../data/payment-method.md) for all methods.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="string" %}
order amount\
\- 0.01 \~ 999999999 -

(refer to amount limit for different [methods](../data/payment-method.md))
{% endswagger-parameter %}

{% swagger-parameter in="body" name="subject" required="true" type="string" %}
payment reason or item title

\- Max. 128 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" type="string" required="true" %}
payment reason detail or item detail. This will be shown on the bank bill.

\- Max. 255 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="trade_type" type="string" required="true" %}
fixed value: WEB
{% endswagger-parameter %}

{% swagger-parameter in="body" name="version" type="string" required="true" %}
fixed value: 2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timeout_express" type="string" %}
m(minutes), h(hours), d(days), c(always end in current day).&#x20;

Used to control the expiration time of **submitting** an order (from initial to processing).  (90m in default, max 15d)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cancellation_express" type="string" %}
m(minutes), h(hours), d(days). The value must be an integer.&#x20;

Used to cancel an order. Ex: 90m Used to control the expiration time of a processing order.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where Pagsmile will send notification to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="return_url" type="sring" %}
web redirect url when payment is finish
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_id" required="true" type="string" %}
merchant user's id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="regions" type="array" %}
regions of the payment. The format is ISO 3166-1 alpha-3\
\- ARG, BRA, etc. Check [here](../data/country-code.md) -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.name" type="string" %}
User's name

\- Will be pre-filled on the checkout page -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.phone" type="string" %}
User's phone

\- Will be pre-filled on the checkout page -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.email" type="string" %}
User's email

\- Will be pre-filled on the checkout page -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.number" type="string" %}
User's identification number

\- Will be pre-filled on the checkout page -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" %}
User's identification type

\- Will be pre-filled on the checkout page -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.zip_code" type="string" %}
zip code

\- Will be pre-filled on the checkout page -
{% endswagger-parameter %}

{% swagger-response status="200" description="submit successfully" %}
```
{
    "code": "10000",
    "msg": "Success",
    "trade_no": "2022010110293900083",
    "out_trade_no": "202201010354003",
    "web_url": "http://checkout-testv2.pagsmile.com?prepay_id=123456",
    "prepay_id":"123456"
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
Check [here](../data/payment-method.md) for supported methods.&#x20;

* If not passing the parameter "method" or pass "method": "", all enabled methods will be shown to the user on the checkout page.
* If passing "method": "PIX", only PIX will be shown to the user on the checkout page.
{% endhint %}

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/create' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
      "charset": "UTF-8",
    * "app_id": "162************38",
    * "out_trade_no": "202201010354002",
    * "order_currency": "BRL",
    * "order_amount": "12.01",
    * "subject": "item name",
    * "content": "item description",
    * "trade_type": "WEB",
      "timeout_express": "1d",
    * "timestamp": "2022-01-01 03:54:01",
    * "notify_url": "http://merchant/callback/success",
    * "buyer_id": "buyer_0101_0001",
    * "version": "2.0",
      "customer": {
          "identify": {
              "type": "CPF",
              "number": "50284414727"
          },
      "name": "Test User Name",
      "email": "test@pagsmile.com"
      },
      "regions": ["BRA"],
      "address": {
          "zip_code": "38082365"
      }
}'
```

{% hint style="danger" %}
Return_url is not required in the request parameters. However if needed, you can overwrite it by appending the return\__url after the web\_url when redirect.&#x20;



`http://checkout.pagsmile.com?prepay_id={$prepay_id}`

↓↓↓

`http://checkout.pagsmile.com?prepay_id={$prepay_id}&return_url=encodeURIComponent({$return_url})`
{% endhint %}

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption><p>The Checkout page without specifying "method"</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption><p>The Checkout page with specifying "method":"PIX" (as an exmaple)</p></figcaption></figure>
