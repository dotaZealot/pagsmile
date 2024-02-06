---
description: How to use Wallet to submit a payin in Colombia.
---

# Wallet

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/trade/pay" method="post" summary="Payin by Wallet" %}
{% swagger-description %}
This endpoint allows you to submit a payin by Wallet in Colombia.
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
\- TPaga, ClaroPay, Dale, Daviplata, Movii, Nequi, Rappipay-
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_currency" required="true" type="string" %}
Fixed value: COP
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="string" %}
payment amount\
\- check [here](../../data/payment-method.md#colombia) for limits -
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

{% swagger-parameter in="body" name="customer.phone" type="string" required="true" %}
User's phone
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.email" type="string" required="true" %}
User's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.number" type="string" required="true" %}
User's identification number

\- NIT: 10 digits, CC: 6\~10 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" required="true" %}
User's identification type

\- NIT or CC -
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
{% tabs %}
{% tab title="TPaga" %}
```
{
    "code": "10000",
    "msg": "Success",
    "prepay_id": "QVUvcG00ZDl6MFVsWkZsTk1IwRDlTZEdnVThOUGxyeHVnZkROND0=-D161Bae8",
    "trade_no": "22022010110293900083",
    "out_trade_no": "202201010354005",
    "web_url": "",
    "trade_status": "PROCESSING",
    "wallet_url": "https://w.tpaga.co/eyJtIjp7Im8iOiJQUiJ9LCJkIjp7InMiOiJQYWdzbWlsZSIsInBydCI6InByLTJlZmYyMzI4NjgxNDNkNjA5OGVlZGJjNGY1YWQ3NjNmMzMxNjdkZmJiYWNkYTc3ZDUxZTgyMzY4ODg4NWRlZTM0ZDViYzM0NyJ9fQ==" //Generate a QR code of this link to allow users scan to pay
}
```
{% endtab %}

{% tab title="ClaroPay" %}
```
{
    "code": "10000",
    "msg": "Success",
    "prepay_id": "QVUvcG00ZDl6MFVsWkZsTk1IwRDlTZEdnVThOUGxyeHVnZkROND0=-D161Bae8",
    "trade_no": "22022010110293900083",
    "out_trade_no": "202201010354005",
    "web_url": "",
    "trade_status": "PROCESSING",
    "pay_url": "https://secure-checkout.payvalida.com?token="
}
```
{% endtab %}

{% tab title="Dale" %}
```
{
    "code": "10000",
    "msg": "Success",
    "prepay_id": "QVUvcG00ZDl6MFVsWkZsTk1IwRDlTZEdnVThOUGxyeHVnZkROND0=-D161Bae8",
    "trade_no": "22022010110293900083",
    "out_trade_no": "202201010354005",
    "web_url": "",
    "trade_status": "PROCESSING",
    "wallet_url": "https://registro.pse.com.co/PSENF/index.html?enc="
}
```
{% endtab %}

{% tab title="Daviplata" %}
```
{
    "code": "10000",
    "msg": "Success",
    "prepay_id": "QVUvcG00ZDl6MFVsWkZsTk1IwRDlTZEdnVThOUGxyeHVnZkROND0=-D161Bae8",
    "trade_no": "22022010110293900083",
    "out_trade_no": "202201010354005",
    "web_url": "",
    "trade_status": "PROCESSING",
    "wallet_url": "https://registro.pse.com.co/PSENF/index.html?enc="
}
```
{% endtab %}

{% tab title="Movii" %}
```
{
    "code": "10000",
    "msg": "Success",
    "prepay_id": "QVUvcG00ZDl6MFVsWkZsTk1IwRDlTZEdnVThOUGxyeHVnZkROND0=-D161Bae8",
    "trade_no": "22022010110293900083",
    "out_trade_no": "202201010354005",
    "web_url": "",
    "trade_status": "PROCESSING",
    "wallet_url": "https://registro.pse.com.co/PSENF/index.html?enc="
}
```
{% endtab %}

{% tab title="Nequi" %}
```
{
    "code": "10000",
    "msg": "Success",
    "prepay_id": "QVUvcG00ZDl6MFVsWkZsTk1IwRDlTZEdnVThOUGxyeHVnZkROND0=-D161Bae8",
    "trade_no": "22022010110293900083",
    "out_trade_no": "202201010354005",
    "web_url": "",
    "trade_status": "PROCESSING",
    "wallet_url": "https://registro.pse.com.co/PSENF/index.html?enc="
}
```
{% endtab %}

{% tab title="Rappipay" %}
```
{
    "code": "10000",
    "msg": "Success",
    "prepay_id": "QVUvcG00ZDl6MFVsWkZsTk1IwRDlTZEdnVThOUGxyeHVnZkROND0=-D161Bae8",
    "trade_no": "22022010110293900083",
    "out_trade_no": "202201010354005",
    "web_url": "",
    "trade_status": "PROCESSING",
    "wallet_url": "https://registro.pse.com.co/PSENF/index.html?enc="
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

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "out_trade_no": "202201010354004",
    * "method": "Wallet",
    * "channel": "TPaga",
    * "order_amount": "12",
    * "order_currency": "COP",
    * "subject": "trade pay test",
      "content": "trade pay test conent",
    * "notify_url": "http://merchant/callback/success",
      "return_url": "https://www.merchant.com",
    * "buyer_id": "buyer_0101_0001",
    * "timestamp": "2022-01-01 03:54:01",
      "timeout_express":"1c",
    * "customer" : {
    *     "identify": {
    *         "type": "NIT",
    *         "number": "1234123121"
          },
    *     "name": "Test User Name",
    *     "email": "test@pagsmile.com",
    *     "phone": "3020481705"
      }
      }'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
