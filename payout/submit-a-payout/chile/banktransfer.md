---
description: How to use Bank Transfer to submit a payout in Chile.
---

# BankTransfer

{% swagger method="post" path="/api/payout" baseUrl="https://sandbox.transfersmile.com" summary="Submit a payout by Bank Transfer in Chile." %}
{% swagger-description %}
This endpoint allows you to submit a payout by Bank Transfer in Chile.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" type="string" required="true" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" required="true" %}
Beneficiary's name, length must between 5 and 100
{% endswagger-parameter %}

{% swagger-parameter in="header" type="string" name="Authorization" required="true" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" type="string" %}
Beneficiary's phone

\- 0 \~ 15 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
Beneficiary 's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="bank_code" type="string" required="true" %}
Bank code, see [_**bank list**_](../../bank-code/bank-in-chile.md)
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="account" required="true" %}
Account, max length is 20

\- 8 \~ 20 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_type" type="string" required="true" %}
Should be one of CHECKING, SAVINGS, VISTA, RUT, SALARY.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_id" type="string" required="true" %}
Beneficiary document id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_type" type="string" required="true" %}
Beneficiary document type, should be one of RUT, RUN, PAS, CE.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" required="true" %}
Fixed Value: BankTransfer
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" type="string" required="true" %}
Merchant's order id

\- Max.50 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" type="string" required="true" %}
One of \[beneficiary | merchant]
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="string" required="true" %}
Payout amount, should be an Integer.

\- Min 1, Max 2,000,000 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount_type" type="string" %}
Specify the amount value is fixed for merchant or beneficiary\
\- One of: source\_amount, arrival\_amount(default) -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" type="string" required="true" %}
Merchant's account currency

\-  supported: USD, GBP, EUR, CLP -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" type="string" required="true" %}
Beneficiary's account currency.

\- Fixed Value: CLP -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where pagsmile will callback to
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="additional_remark" required="true" %}
Additional Remark\
\- Max Length: 40 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="country" required="true" %}
Fixed value: CHL, for Chile
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="success" %}
```javascript
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQBCL",
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
    "data": {
        "err": "error detail message"
    }
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="unautorized" %}
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
    "data": {
        "err": "error detail message"
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
    * "bank_code": "012", // Banco del Estado de Chile
    * "account" : "00219400254640654321", // just for test in sandbox
    * "account_type" : "CHECKING",
    * "document_id" : "123456789", // just for test in sandbox, don't use this in production.
    * "document_type" : "RUT",
    * "method" : "BankTransfer",
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

## Example of Document

{% hint style="info" %}
* RUT / RUN numbers have eight digits, plus a verification digit, and are generally written in this format: xxxxxxxx-z. Z can be a digit or the letter K. For example 3\*\*\*\*\*\*7-K,  7\*\*\*\*\*\*8-5. **Only send alphanumeric values in the API**, like 3\*\*\*\*\*\*7K.
* For individuals, RUT is the same as RUN. For businesses, they only have RUT.
{% endhint %}

<table><thead><tr><th width="173">Document Type</th><th width="133">Document ID</th><th width="229">Format</th><th width="418">Description</th><th></th></tr></thead><tbody><tr><td>RUT</td><td>1*******6</td><td>9 digits</td><td>A RUT <em>(Rol Único Tributario)</em> is the individual tax ID number</td><td></td></tr><tr><td>RUN</td><td>2*******8</td><td>9 digits</td><td>A RUN <em>(Rol Único Nacional)</em> is a unique identification number given to every Chilean resident, foreign resident, and anyone who stays in Chile on anything other than a tourist visa</td><td></td></tr><tr><td>CE</td><td>3********9</td><td>between 9 and 16 digits</td><td>Carnet de Extranjería</td><td></td></tr><tr><td>PASS</td><td>4********0</td><td>between 9 and 16 digits</td><td>Passport</td><td></td></tr></tbody></table>

## Example of Account

{% hint style="info" %}
Account type "RUT" is a very simple account that people starting in banking can have that is associated with their tax ID, usually for people getting benefits from the government.&#x20;

Account type "VISTA" is like a savings account but without the option to gain interest on your funds, often used for companies to pay salaries to their employees.
{% endhint %}

| Bank                      | Bank Code | Description                                                        |
| ------------------------- | --------- | ------------------------------------------------------------------ |
| Banco del Estado de Chile | 012       | If the type of account is "RUT Account": Account must be 8 digits. |
| Others                    |           | 7 - 20 digits                                                      |
