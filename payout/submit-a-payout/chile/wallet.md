---
description: Where to use Vita wallet to submit a payout in Chile.
---

# Wallet

{% swagger method="post" path=" " baseUrl="https://sandbox.transfersmile.com/api/payout" summary="Submit a payout by Wallet in Chile" %}
{% swagger-description %}
This endpoint allows you to submit a payout by e-Wallet in Chile.
{% endswagger-description %}

{% swagger-parameter in="header" type="string" name="Content-Type" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" type="string" required="true" name="AppId" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" %}
Beneficiary's name

\- Min.5 Max.100 -
{% endswagger-parameter %}

{% swagger-parameter in="header" type="string" required="true" name="Authorization" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" type="string" %}
Beneficiary's phone.

\- 0 \~ 15 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
Beneficiary's email

\- Max.64 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" type="string" required="true" %}
Beneficiary Vita account.

\- 0 \~ 64 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_type" type="string" required="true" %}
Fixed Value: EMAIL
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="document_id" %}
Beneficiary document id
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="document_type" %}
Beneficiary document type
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="methd" required="true" %}
Fixed Value: WALLET
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="channel" required="true" %}
Fixed Value: Vita
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="custom_code" required="true" %}
Merchant's order id

\- Max.50 -
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="fee_bear" required="true" %}
One of \[beneficiary | merchant]
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="amount" required="true" %}
Payout amount, should be an Integer.

\- Min 1, Max 2,000,000 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount_type" type="string" required="false" %}
Specify the amount value is fixed for merchant or beneficiary\
\- One of: source\_amount, arrival\_amount(default) -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" type="string" required="true" %}
Merchant's account currency

\- supported: USD, GBP, EUR, CLP - &#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" type="string" required="true" %}
Beneficiary's account currency.

\- Fixed Value: CLP -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where pagsmile will callback to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additional_remark" type="string" required="true" %}
Additional Remark\
\- Max length: 40 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="country" required="true" %}
Beneficiary's Country

\- Fixed Value: CHL -&#x20;
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="submit successfully" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQWCL",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "100",
        "arrival_currency": "CLP",
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

{% swagger-response status="500: Internal Server Error" description="system error" %}
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

## Example of Document

{% hint style="info" %}
* RUT / RUN numbers have eight digits, plus a verification digit, and are generally written in this format: xxxxxxxx-z. Z can be a digit or the letter K. For example 3\*\*\*\*\*\*7-K,  7\*\*\*\*\*\*8-5. **Only send alphanumeric values in the API**, like 3\*\*\*\*\*\*7K.
* For individuals, RUT is the same as RUN. For businesses, they only have RUT.
{% endhint %}

<table><thead><tr><th width="176">Document Type</th><th width="160">Document ID</th><th width="135">Description</th><th width="405"></th><th></th></tr></thead><tbody><tr><td>RUT</td><td>7******85</td><td>9 digits</td><td>A RUT <em>(Rol Único Tributario)</em> is the individual tax ID number </td><td></td></tr><tr><td>RUN</td><td>7******85</td><td>9 digits</td><td>A RUN <em>(Rol Único Nacional)</em> is a unique identification number given to every Chilean resident, foreign resident, and anyone who stays in Chile on anything other than a tourist visa</td><td></td></tr></tbody></table>

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
    * "account" : "g******me@gmail.com",
    * "account_type" : "EMAIL",
      "document_id" : "************",
      "document_type" : "***",
    * "method" : "WALLET",
    * "channel" : "Vita",
    * "custom_code" : "custom_code9982674851738108",
    * "fee_bear" : "merchant",
    * "amount" : "100", //Amount should be an integer, like 1.00 is not available.
    * "source_currency" : "CLP",
    * "arrival_currency" : "CLP",
    * "notify_url" : "https://notify.url",
    * "additional_remark" : "pagsmile payout test",
    * "country": "CHL"
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}
