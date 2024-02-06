---
description: Where to submit a payout by Wallet in Colombia.
---

# Wallet



{% swagger method="post" path=" " baseUrl="https://sandbox.transfersmile.com/api/payout" summary=" Submit a payout by Wallet in Colombia" %}
{% swagger-description %}
This endpoint allows you to submit a payout by e-Wallet in Colombia.
{% endswagger-description %}

{% swagger-parameter in="header" type="string" name="Content-Type" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" type="string" name="AppId" required="true" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="header" type="string" name="Authorization" required="true" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" %}
Beneficiary's name

\- Min.5 Max.100 -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="phone" %}
Beneficiary's phone.

\- 0 \~ 15 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="email" %}
Beneficiary's email

\- Max.64 -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="document_id" %}
Beneficiary document id
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="document_type" %}
Beneficiary document type
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="account" required="true" %}
Beneficiary Tpaga account.

\- 11 \~ 14 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="account_type" required="true" %}
Fixed Value: PHONE
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" required="true" %}
Fixed Value: WALLET
{% endswagger-parameter %}

{% swagger-parameter in="body" name="channel" type="string" required="true" %}
Fixed Value: Tpaga
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" type="string" required="true" %}
Merchant's order id

\- Max. 50 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" type="string" required="true" %}
One of \[beneficiary | merchant]
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="string" required="true" %}
Payout Amount, should be an Integer.

\- Min 1, Max 10,000,000 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount_type" type="string" %}
Specify the amount value is fixed for merchant or beneficiary\
\- One of: source\_amount, arrival\_amount(default) -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" type="string" required="true" %}
Merchant's account currency

\- supported: USD, GBP, EUR, COP - &#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" type="string" required="true" %}
Beneficiary's account currency.

\- Fixed Value: COP -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where pagsmile will callback to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additional_remark" type="string" required="true" %}
Additional Remark\
\- Max length: 40 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" required="true" type="string" %}
Beneficiary's Country

\- Fixed Value: COL -&#x20;


{% endswagger-parameter %}

{% swagger-response status="200: OK" description="submit successfully" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQWC",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "100",
        "arrival_currency": "COP",
        "source_amount": "0.07",
        "source_currency": "USD",
        "status": "IN_PROCESSING"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="bad request" %}
```javascript
{
    "code": 4001000,
    "msg": "invalid parameter",
    "time": 1637224716,
    "data": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="unauthorized" %}
```javascript
{
    "code": 4004003,
    "msg": "permission denied",
    "time": 1637224716,
    "data": {}
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="fee not configured" %}
```javascript
{
    "code": 5001003,
    "msg": "fee not configured",
    "time": 1637224716,
    "data": {
        ... ...
    }
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="balance insufficient" %}
```javascript
{
    "code": 5001102,
    "msg": "balance insufficient",
    "time": 1637224716,
    "data": {
        ... ...
    }
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="server error" %}
```javascript
{
    "code": 5001000,
    "msg": "system error",
    "time": 1637224716,
    "data": {}
}
```
{% endswagger-response %}
{% endswagger %}

## Example

```
curl --location --request POST 'https://sandbox.transfersmile.com/api/payout' \
--header 'AppId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
      "name" : "GUILHERME ****** SOUZA",
      "phone" : "468****068",
      "email" : "g******me@gmail.com",
    * "account" : "+57317****412",
    * "account_type" : "PHONE",
      "document_id" : "************",
      "document_type" : "***",
    * "method" : "WALLET",
    * "channel" : "Tpaga",
    * "custom_code" : "custom_code9982674851738108",
    * "fee_bear" : "merchant",
    * "amount" : "100", //Amount should be an integer, like 1.00 is not available.
    * "source_currency" : "COP",
    * "arrival_currency" : "COP",
    * "notify_url" : "https://notify.url",
    * "additional_remark" : "pagsmile payout test",
    * "country": "COL"
}'


```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

{% hint style="success" %}
In **sandbox** environment, please use _<mark style="color:red;">**+57311111111**</mark>_ as  <mark style="color:blue;">**Tpaga**</mark> account for testing **Failed** payout, any other <mark style="color:blue;">**Tpaga**</mark> account will be successful.
{% endhint %}
