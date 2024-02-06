---
description: Where to submit a payout by SPEI in Mexico.
---

# SPEI

{% swagger baseUrl="https://sandbox.transfersmile.com" path="/api/payout" method="post" summary="Submit a payout by SPEI in Mexico" %}
{% swagger-description %}
This endpoint allows you to submit a payout by SPEI in Mexico.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" type="string" required="true" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" required="true" %}
beneficiary's name, length must between 5 and 40
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" type="string" %}
beneficiary's phone

\- 0 \~ 15 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
beneficiary 's email&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="bank_code" type="number" required="true" %}
bank code, see [_**bank list**_](../../bank-code/bank-in-mexico.md)

_**-**_ Required when account\_type is **not** **clabe** -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" type="number" required="true" %}
account

\- 10 \~ 18 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_type" type="string" required="true" %}
one of \[debit | phone | clabe]
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_id" type="string" required="true" %}
beneficiary document id&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_type" type="string" required="true" %}
one of \[RFC | CURP ]
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" required="true" %}
payout method, e.g. SPEI
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" type="string" required="true" %}
merchant payout id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" type="string" required="true" %}
one of \[beneficiary | merchant]&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="number" required="true" %}
Payout Amount, 2 decimal numbers

\- Min 0.01, Max 400,000 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" type="string" required="true" %}
Merchant Account Currency\
One of: USD, EUR, GBP, MXN&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" type="string" required="true" %}
MXN for Mexico
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where pagsmile will callback to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additional_remark" type="string" required="true" %}
Additional Remark\
\- Max Length: 40 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" type="string" required="true" %}
MEX for Mexico
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="submit successfully." %}
```
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "S202108100734054iRiUZFPXfQM",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "0.51",
        "arrival_currency": "MXN",
        "source_amount": "0.07",
        "source_currency": "USD",
        "status": "IN_PROCESSING"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="order already existed." %}
```
{
    "code": 4001010,
    "msg": "order already existed",
    "time": 1628580940,
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
    "data": {
        ... ...
    }
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
    "data": {
        ... ...
    }
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
    * "name" : "GUILHERME ****** SOUZA",
      "phone" : "468****068",
      "email" : "g******me@gmail.com",
    * "bank_code" : "40002",
    * "account" : "002010077777777771",
    * "account_type" : "clabe",
    * "document_id" : "CUP800****691",
    * "document_type" : "RFC",
    * "method" : "SPEI", // fixed value: SPEI
    * "custom_code" : "custom_code9982674851738108", // merchant order id
    * "fee_bear" : "merchant",
    * "amount" : "0.51",
    * "source_currency" : "MXN",
    * "arrival_currency" : "MXN", // fixed value: MXN
    * "notify_url" : "https://notify.url",
    * "additional_remark" : "pagsmile payout test remark",
    * "country" : "MEX" // fixed value: MEX
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

{% hint style="success" %}
In **sandbox** environment, please use _<mark style="color:green;">**002010077777777771**</mark>_ as  <mark style="color:blue;">**SPEI**</mark> account for testing **PAID** payout,  and the account _<mark style="color:red;">**014027000005555558**</mark>_ for testing **FAILED** payout.
{% endhint %}

## Example of SPEI account <a href="#example-of-pix-account" id="example-of-pix-account"></a>

| Account Type | Account            |           |
| ------------ | ------------------ | --------- |
| clabe        | 112233445566778899 | 18 digits |
| debit        | 1122334455667788   | 16 digits |
| phone        | 5522123456         | 10 digits |

{% tabs %}
{% tab title="Mexico document type" %}
Mexican taxpayers could get RFC.&#x20;

RFCs are 13 digits long for individuals, 12 for companies, and they’re made up of letters and numbers. The first 4 digits for individuals, or 3 for companies, are taken from the name, then there are six numbers denoting the date of birth or when the business was founded, and the end digits are check digits.



Mexican citizen or resident could get CURP.

It’s an 18-digit social security number for people living in Mexico. The 18 characters combine information deriving from your name, date and place of birth, and gender to create a unique code.


{% endtab %}

{% tab title="Mexico bank account" %}
The first three digits of the bank account should be the last three digits of the bank code.&#x20;

<pre><code>"bank_code":"90<a data-footnote-ref href="#user-content-fn-1">646</a>",
"account":"<a data-footnote-ref href="#user-content-fn-2">646</a>18**********1800"
</code></pre>
{% endtab %}
{% endtabs %}













[^1]: 

[^2]: 
