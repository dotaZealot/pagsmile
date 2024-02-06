---
description: How to create a card payment.
---

# Create Card Payment

## **Create Card Payment**

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/trade/pay" method="post" summary="Payin by CreditCard" %}
{% swagger-description %}
This endpoint allows you to create a card payment.
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
Fixed value: BRL&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="string" %}
payment amount\
\- 0.5\~50000 BRL -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="subject" required="true" type="string" %}
payment reason or item title

\- Max. 128 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" type="string" required="true" %}
payment reason detail or item detail. This will be shown on the bank bill.

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
use [Pagsmile Javascript](../tools/pagsmile-javascript.md) to get toekn
{% endswagger-parameter %}

{% swagger-parameter in="body" name="issuer" required="true" type="string" %}
issuer of CreditCard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="installments" type="string" %}
installments for CreditCard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="website_url" type="string" %}
merchant website URL

\- Max. 128 chars -
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

\- 11 digits if CPF or 14 digits if CNPJ -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" required="true" %}
User's identification type

\- CPF or CNPJ -
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

{% swagger-parameter in="body" name="threeds.version" type="string" required="false" %}
Version used in the transaction
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.cavv" type="string" required="true" %}
Authentication Value (CAVV / AAV for 3DS1) recieved from authorization/Authentication response
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.eci" type="string" required="true" %}
ECI value recieved from authorization/authentication response
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.server_trans_id" type="string" required="false" %}
Universally unique transaction identifier assigned by the 3DS Server to identify a single transaction generated by the Init 3DS API and used to link the init call to the order call
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.acs_trans_id" type="string" %}
This field contains a universally unique transaction identifier assigned by the ACS to identify a single transaction.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.ds_trans_id" type="string" %}
A universally unique transaction identifier is assigned by the DS to identify a single transaction.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.status" type="string" %}
3DSecure - Status text received from 3D secure vendor
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.status_code" type="string" required="false" %}
3DSecure - Status code recieved from authorization/authentication response, (Possible values: U, N, Y, A, C, D, R, I)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.status_reason_code" type="string" %}
String EMVCO Indicator of the reason for the 3DS status code provided during the authentication, (Possible values: 01, 02, 03, 04, 05, 06, 07, 08, 09, 10, 11, 12, 13, 14, 15, 16)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.liability_shift" type="string" %}
liability shift - indicate whether the chargeback liability shifted to the card issuer
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

### Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "162************38",
    "out_trade_no": "202201010354003",
    "method": "CreditCard",
    "order_amount": "12.01",
    "order_currency": "BRL",
    "subject": "trade pay test",
    "content": "trade pay test conent",
    "notify_url": "http://merchant/callback/success",
    "return_url": "https://www.merchant.com",
    "buyer_id": "buyer_0101_0001",
    "user_ip":"127.0.0.1",
    "token":"${token}",
    "issuer":"visa",
    "installments":"1",
    "timestamp": "2022-01-01 03:54:01",
    "timeout_express":"1c",
    "customer" : {
        "identify": {
            "type": "CPF",
            "number": "50284414727"
        },
        "name": "Test User Name",
        "email": "test@pagsmile.com",
        "phone": "75991435892"
    },
    "address" : {
        "zip_code": "38082365",
    },
    "threeds": {
          "version":"2.1.0",
          "cavv":"MTIzNDU2Nzg5MDEyMzQ1Njc4OTA",
          "eci":"05",
          "server_trans_id":"1111-2222-3333-4444",
          "acs_trans_id":"7777-8797-4645-1233",
          "ds_trans_id":"7777-8797-4645-1233",
          "status":"Cardholder authenticated",
          "status_code":"Y",
          "status_reason_code":"15",
          "liability_shift":"true"
    }
}'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
