---
description: How to use Wallet to submit a payin in Chile.
---

# Wallet

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/trade/pay" method="post" summary="Payin by Wallet" %}
{% swagger-description %}
This endpoint allows you to submit a payin by Wallet in Chile.
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
Fixed value: Wallet
{% endswagger-parameter %}

{% swagger-parameter in="body" name="channel" type="string" required="true" %}
Wallet type\
\- Mach or Chek -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_currency" required="true" type="string" %}
Fixed value: CLP
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="string" %}
payment amount\
\- check [here](../../data/payment-method.md#chile) for limits -
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
User's identification number

\- 9 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" required="true" %}
User's identification type

\- RUT or RUN -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.zip_code" required="false" type="string" %}
zip code\
\- 7 digits -
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
{% tabs %}
{% tab title="Mach" %}
```
{
    "code": "10000",
    "msg": "Success",
    "trade_no": "2022010110293900083",
    "out_trade_no": "202201010354006",
    "web_url": "",
    "trade_status": "PROCESSING",
    "app_link_url": "machapp://pay-biz/payment/3e51efda-d80d-41c9-8fb1-2454a7cbc7e6"
}
```
{% endtab %}

{% tab title="Chek" %}
```
{
    "code": "10000",
    "msg": "Success",
    "trade_no": "2022010110293900083",
    "out_trade_no": "202201010354006",
    "web_url": "",
    "trade_status": "PROCESSING",
    "pay_url": "https://app.payku.cl/gateway/cobro?id=trx12cfab0b34da56b0f&valid=78aecf9012"
}
```
{% endtab %}
{% endtabs %}
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
**Payment Tips**

* If you receive "app\_link\_url" in the response, it will redirect users to the app on mobile. For products on the desktop, you can use this URL to generate a QR code to let users scan.
{% endhint %}

<figure><img src="../../../.gitbook/assets/微信图片_20230727181614.png" alt=""><figcaption><p>Example of payment page</p></figcaption></figure>

## Example of identify

{% hint style="info" %}
* RUT / RUN numbers have eight digits, plus a verification digit, and are generally written in this format: xxxxxxxx-z. Z can be a digit or the letter K. For example 3\*\*\*\*\*\*7-K,  7\*\*\*\*\*\*8-5. **Only send alphanumeric values  in the API**, like 3\*\*\*\*\*\*7K.
* For individuals, RUT is the same as RUN. For businesses, they only have RUT.
{% endhint %}

<table><thead><tr><th width="154">Identify Type</th><th width="160">Identify Number</th><th width="135">Description</th><th width="405"></th><th></th></tr></thead><tbody><tr><td>RUN</td><td>7******85</td><td>9 digits</td><td>A RUN <em>(Rol Único Nacional)</em> is a unique identification number given to every Chilean resident, foreign resident, and anyone who stays in Chile on anything other than a tourist visa</td><td></td></tr><tr><td>RUT</td><td>7******85</td><td>9 digits</td><td>A RUT <em>(Rol Único Tributario)</em> is the individual tax ID number</td><td></td></tr></tbody></table>

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "out_trade_no": "202201010354006",
    * "method": "Wallet",
    * "channel": "Mach",
    * "order_amount": "12.01",
    * "order_currency": "CLP",
    * "subject": "trade pay test",
      "content": "trade pay test conent",
    * "notify_url": "http://merchant/callback/success",
      "return_url": "https://www.merchant.com",
    * "buyer_id": "buyer_0101_0001",
    * "timestamp": "2022-01-01 03:54:01",
      "timeout_express":"1c",
    * "customer" : {
    *     "identify": {
    *         "type": "RUT",
    *         "number": "220604497"
          },
    *     "name": "Test User Name",
    *     "email": "test@pagsmile.com"
      }'
```



{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
