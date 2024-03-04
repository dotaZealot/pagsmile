---
description: How to use Pagsmile Checkoutpage to submit a payin.
---

# All-In-One Checkout

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
Add this object to show only the selected method. For instance, “method”: “PIX” will only show the PIX method. To show all the methods do not add this object in the request body. Check [here](../data/payment-method.md) for all methods.
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

{% swagger-parameter in="body" name="regions" type="array" required="false" %}
regions of the payment. The format is ISO 3166-1 alpha-3\
\- Check [here](../data/country-code.md) to check -&#x20;
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

## Options

All-In-One Checkout is for querying Pagsmile checkout page (payment wall) to present one or all available payment methods to users. It is the most sample way for integrating for all countries and methods of Pagsmile.

* [**General**](general.md)
  * More detailed examples for querying Pagsmile checkout page for general merchants.
* [**E-Commerce**](../../payout/submit-a-payout/paypal/)
  * More detailed examples for querying Pagsmile checkout page for E-com merchants.
