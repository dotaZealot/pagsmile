---
description: How to use Bank Transfer to submit a payout in Brazil.
---

# BankTransfer

{% swagger baseUrl="https://sandbox.transfersmile.com" path="/api/payout" method="post" summary="Submit a payout by Bank Transfer in Brazil" %}
{% swagger-description %}
This endpoint allows you to submit a payout by Bank Transfer in Brazil.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" type="string" required="true" %}
Your App ID in payout platform.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" required="true" %}
Beneficiary's name\
\- Length must between 5 and 100 -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" type="string" %}
Beneficiary's phone

\- 0 \~ 15 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
Beneficiary's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_id" type="string" required="true" %}
Beneficiary's personal identification number.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_type" type="string" required="true" %}
Beneficiary's personal identification type

\- One of: CPF, CNPJ -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="bank_code" type="string" required="true" %}
Bank Code in Brazil, see [_**bank list**_](../../bank-code/bank-in-brazil.md)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="branch" type="string" required="true" %}
Bank Branch Code

\- 4 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" type="string" required="true" %}
Beneficiary's Bank Account

\- 4 \~ 18 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_type" type="string" required="true" %}
Beneficiary's Account Type\
\- One of: SAVINGS, CHECKING -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_digit" type="string" required="false" %}
Account Digit

\- 1 or 2 digits. Left empty if the account\_digit is included in the account field -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="branch_digit" type="string" %}
Branch digit
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" required="true" %}
Fixed value: BANKTRANSFER
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" type="string" required="true" %}
Merchant Payout ID\
\- Max. 50 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" type="string" required="true" %}
Processing fee charges to merchant or beneficiary\
\- One of: merchant, beneficiary -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="number" required="true" %}
Payout Amount, 2 decimal numbers

\- Min 0.50, Max 50,000 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount_type" type="string" %}
Specify the amount value is fixed for merchant or beneficiary\
\- One of: source\_amount, arrival\_amount(default) -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" type="string" required="true" %}
Merchant Account Currency\
\- One of: USD, EUR, GBP, BRL -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" type="string" required="true" %}
Fixed value: BRL
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where pagsmile will send notification to.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additional_remark" type="string" required="true" %}
Descriptor on the user's bank bill\
\- Max. 40 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" type="string" required="true" %}
BRA for Brazil
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="submit successfully" %}
```
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQM",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "0.51",
        "arrival_currency": "BRL",
        "source_amount": "0.07",
        "source_currency": "USD",
        "status": "IN_PROCESSING"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="order already existed" %}
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
      "phone": "",
      "email": "payout@pagsmile.com",
    * "bank_code": "001",
    * "account_type": "CHECKING", // should be one of SAVINGS, CHECKING
    * "account": "6***84", // "4" is the account digit
      "account_digit": "",
    * "branch": "0**8",
    * "document_id": "12*******91",
    * "document_type": "CPF",  // should be one of CPF, CNPJ
    * "source_currency": "BRL", 
    * "arrival_currency": "BRL", // fixed value: BRL
    * "fee_bear": "merchant", // should be one of merchant, beneficiary
    * "method": "BANKTRANSFER", // fixed value: BANKTRANSFER
    * "amount": "1.80",
    * "notify_url": "https://notify.url",
    * "custom_code" : "custom_code9982674851738108",
    * "additional_remark": "pagsmile payout test remark",
    * "country": "BRA"  // fixed value: BRA
}
'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

## Example of Document

| Document Type | Document ID              | Descritpion |
| ------------- | ------------------------ | ----------- |
| CPF           | 22\*\*\*\*\*\*\*99       | 11 digits   |
| CNPJ          | 23\*\*\*\*\*\*\*\*\*\*31 | 14 digits   |

## Example of Brazil Bank Account

* X --> Numeric character
* D --> Alphanumeric character

<table><thead><tr><th width="128">Bank code</th><th width="152">Bank name</th><th width="146">Bank branch</th><th width="168">Checking account</th><th>Savings account</th></tr></thead><tbody><tr><td>001</td><td>Banco do Brasil S.A.</td><td>XXXX, XXXXD or XXXX-D</td><td>XXXXXXXX or XXXXXXXX-X</td><td>XXXXXXXXX or XXXXXXXXX-X Prefixes: 00, 01, 51, 02, 52, 91, 92, 96 or 97</td></tr><tr><td>033</td><td>Banco Santander Brasil S.A.</td><td>XXXX</td><td>XXXXXXXX-X Prefixes: 01, 02, 03, 05, 09, 13 or 92</td><td>XXXXXXXX-X Prefixes: 60</td></tr><tr><td>104</td><td>Caixa CEF</td><td>XXXX, XXXXX or XXXX-X</td><td>XXX.XXXXXXXX-X or any combination with or without ',' or '-' characters and prefix or verification code Prefixes: 001, 010, 003 or 023 </td><td>XXXX.XXXXXXXXX-X //XXX.XXXXXXXX-X or any combination with or without ',' or '-' characters and prefix or verification code Prefixes: 1288 or 013, 022</td></tr><tr><td>237</td><td>Banco Bradesco S.A.</td><td>XXXX, XXXXX or XXXX-X</td><td>XXXXXXX or XXXXXXX-X</td><td>XXXXXXX or XXXXXXX-X</td></tr><tr><td>341</td><td>Itau Unibanco S.A.</td><td>XXXX</td><td>XXXXX-X</td><td>XXXXX-X</td></tr><tr><td>399</td><td>HSBC Bank Brasil S.A.</td><td>XXXX, XXXXD, XXXXDD, XXXX-D or XXXX-DD</td><td>XXXXX-XX</td><td>XXXXX-XX</td></tr><tr><td>-</td><td>Other banks</td><td>XXXX, XXXXD, XXXXDD, XXXX-D or XXXX-DD</td><td>-</td><td>-</td></tr></tbody></table>

{% hint style="info" %}
"account\_digit" is optional. If the user fills full account number in the "account" field, the "account\_digit" field should be removed or left empty. For example, if the complete account number is 1234-5, then the request can be

`"account": "12345"`

or

`"account": "1234",`

`"account_digit": "5"`
{% endhint %}

## Third-party CPF/CNPJ Validator

* <mark style="color:blue;">**Go:**</mark> [https://github.com/paemuri/brdoc](https://github.com/paemuri/brdoc)
* <mark style="color:blue;">**Java:**</mark> [https://github.com/LuisGuadagnin/cpf-cnpj-handler](https://github.com/LuisGuadagnin/cpf-cnpj-handler)
* <mark style="color:blue;">**Online:**</mark> [https://4app.net/tools/validator/document/cpf\_validator](https://4app.net/tools/validator/document/cpf\_validator)
