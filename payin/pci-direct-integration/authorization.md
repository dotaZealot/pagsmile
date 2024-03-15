---
description: How to create an authorization.
---

# Authorization

{% swagger method="post" path="/trade/pre-authorization" baseUrl="https://gateway-test.pagsmile.com" summary="Authorization" %}
{% swagger-description %}
This endpoint allows you to create an authorization.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; chartset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="app_id" required="true" %}
created app's id at dashboard

\- Max. 32 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" type="string" required="true" %}
yyyy-MM-dd HH:mm:ss\
\- Max. 19 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="format" type="string" required="true" %}
Fixed value: JSON
{% endswagger-parameter %}

{% swagger-parameter in="body" name="out_trade_no" type="string" required="true" %}
ID given by the merchant in their system\
\- Max. 64 chars -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" required="true" %}
Fixed value: CreditCard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="number" %}
payment amount
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_currency" type="string" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="subject" type="string" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="trade_type" type="string" required="true" %}
Fixed value: API
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where Pagsmile will send notification to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="return_url" type="string" %}
Redirect to Merchant's url when user finished checkout
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_id" required="true" type="string" %}
buyer id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timeout_express" type="string" %}
m(minutes), h(hours), d(days), c(always end in current day).&#x20;

Used to control the expiration time of **submitting** an order (from initial to processing).  (90m in default, max 15d)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" type="string" required="true" %}
The token received from Tokenization API.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="version" type="string" required="false" %}
Fixed value: 2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="website_url" type="string" required="false" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="issuer" type="string" required="true" %}
issuer of the card.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.sli" required="true" type="string" %}
Security level indicator
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.version" required="true" type="string" %}
The version of the 3D Secure that was used for authentication
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.cavv" required="true" type="string" %}
Authentication Value (CAVV / AAV for 3DS1) recieved from authorization/Authentication response
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.eci" required="true" type="string" %}
ECI value recieved from authorization/authentication response
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.acs_trans_id" type="string" required="true" %}
This field contains a universally unique transaction identifier assigned by the ACS to identify a single transaction.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.ds_trans_id" type="string" required="true" %}
A universally unique transaction identifier is assigned by the DS to identify a single transaction.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.status" type="string" required="true" %}
3DSecure - Status text received from 3D secure vendor
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.status_code" required="true" type="string" %}
3DSecure - Status code recieved from authorization/authentication response, (Possible values: U, N, Y, A, C, D, R, I)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.status_reason_code" type="string" required="true" %}
String EMVCO Indicator of the reason for the 3DS status code provided during the authentication, (Possible values: 01, 02, 03, 04, 05, 06, 07, 08, 09, 10, 11, 12, 13, 14, 15, 16)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="threeds.liability_shift" type="string" required="true" %}
liability shift - indicate whether the chargeback liability shifted to the card issuer
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Authorization" type="string" %}
Basic Base($app\__id:$security\__key)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="submit successfully" %}
```json
{
    "msg": "Success",
    "code": "10000",
    "out_trade_no": "8335***600",
    "web_url": "",
    "trade_no": "2022***215",
    "prepay_id": "MnFrV****OD0=-a220184D"

}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="invalid signature" %}
```json
{
    "code":"40002",
    "msg":"Business Failed",
    "sub_code":"invalid-signature",
    "sub_msg":"invalid signature"
}
```
{% endswagger-response %}
{% endswagger %}

### Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pre-authorization' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "1617****8052",
    * "timestamp": "2022-08-11 10:25:46",
    * "format": "JSON",
    * "out_trade_no": "out_181***1300",
    * "method": "CreditCard",
    * "order_amount": "120",
    * "order_currency": "BRL",
    * "subject": "Cobrança única digital",
    * "content": "trade pay test conent",
    * "trade_type": "API",
    * "notify_url": "http://demo.gemini-tiger.cn/callback/success",
      "return_url": "http://demo.gemini-tiger.cn/test",
    * "buyer_id": "buyer_0810",
      "timeout_express":"30m",
    * "token":"psct_b67******ecad89a5de",
      "version": "2.0",
      "website_url": "www.xcloud.com",
    * "issuer": "VISA",
    * "threeds": {
    *       "version":"2",
    *       "cavv":"MTIzNDU2Nzg5MDEyMzQ1Njc4OTA",
    *       "eci":"05",
    *       "acs_trans_id":"7777-8797-4645-1233",
    *       "ds_trans_id":"7777-8797-4645-1233",
    *       "status":"Cardholder authenticated",
    *       "status_code":"Y",
    *       "status_reason_code":"15",
    *       "liability_shift":"true"
      },
}'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
