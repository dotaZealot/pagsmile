---
description: How to use Pix to submit a payout in Brazil.
---

# Pix

{% swagger baseUrl="https://sandbox.transfersmile.com" path="/api/payout" method="post" summary="Submit a payout by PIX in Brazil." %}
{% swagger-description %}
This endpoint allows you to submit a payout by PIX in Brazil.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; chartset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" type="string" required="true" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" required="true" %}
Beneficiary's name\
\- Length between 5 and 100 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" type="string" %}
Beneficiary's phone

\- 0 \~ 15 digits -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
Beneficiary's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_id" type="string" required="true" %}
Beneficiary's personal identification number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_type" type="string" required="true" %}
Beneficiary's personal identification type

\- One of: CPF, CNPJ -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" type="string" required="true" %}
Beneficiary's PIX account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_type" type="string" required="true" %}
Beneficiary's PIX account type\
\- One of: CPF, CNPJ, EVP, PHONE, EMAIL -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" required="true" %}
Fixed value: PIX
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" type="string" required="true" %}
Merchant Payout ID\
\- Max. 50 chars -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" type="string" required="true" %}
Processing fee charges to merchant or beneficiary.\
\- One of: merchant beneficiary -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="number" required="true" %}
Payout Amount, 2 decimal numbers

\- Min 0.01, Max 50,000 - &#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount_type" %}
Specify the amount value is fixed for merchant or beneficiary\
\- One of: source\_amount, arrival\_amount(default) -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" type="string" required="true" %}
Merchant Account Currency\
\- One of: USD, EUR, GBP, BRL -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" type="string" required="true" %}
Fixed value: BRL&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where pagsmile will send notification to.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additional_remark" type="string" required="true" %}
Descriptor on the user's bank bill\
\- Max length: 40 -
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
// system error
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

## Example

```
curl --location --request POST 'https://sandbox.transfersmile.com/api/payout' \
--header 'AppId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "name": "GUILHERME ****** SOUZA",
      "phone": "",
      "email": "payout@pagsmile.com",
    * "amount": 150,
    * "arrival_currency": "BRL", // fixed value: BRL
    * "custom_code" : "custom_code_your_order_id",
    * "document_id": "22*******99",
    * "document_type": "CPF",
    * "fee_bear": "merchant",
    * "method": "PIX",   // fixed value: PIX
    * "notify_url": "https://notify.url",
    * "account": "22*******99",
    * "account_type": "CPF",  // should be one of CPF CNPJ PHONE EMAIL EVP
    * "source_currency": "BRL", 
    * "additional_remark": "pagsmile payout test remark",
    * "country": "BRA" // fixed value: BRA
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

{% hint style="success" %}
In **sandbox** environment, please use _<mark style="color:red;">**`pagsmile_test_reject@pagsmile.com`**</mark>_ as  **PIX** _account_, and **EMAIL** as _account\_type_ for testing <mark style="color:red;">REJECTED</mark> payout, any other **PIX** account will be success (<mark style="color:green;">PAID</mark>).&#x20;

The document\_id should be valid to pass the system.
{% endhint %}

## Example of Document

| Document Type | Document ID              | Description |
| ------------- | ------------------------ | ----------- |
| CPF           | 22\*\*\*\*\*\*\*99       | 11 digits   |
| CNPJ          | 23\*\*\*\*\*\*\*\*\*\*31 | 14 digits   |

## Third-party CPF/CNPJ Validator

* <mark style="color:blue;">**Go:**</mark> [<mark style="color:blue;">https://github.com/paemuri/brdoc</mark>](https://github.com/paemuri/brdoc)
* <mark style="color:blue;">**Java:**</mark> [<mark style="color:blue;">https://github.com/LuisGuadagnin/cpf-cnpj-handler</mark>](https://github.com/LuisGuadagnin/cpf-cnpj-handler)
* <mark style="color:blue;">**Online:**</mark> [<mark style="color:blue;">https://4app.net/tools/validator/document/cpf\_validator</mark>](https://4app.net/tools/validator/document/cpf\_validator)

## Example of PIX account

<table><thead><tr><th width="249.33333333333331">Account Type</th><th>Account</th><th>Description</th></tr></thead><tbody><tr><td>CPF</td><td>22*******99</td><td>11 digits</td></tr><tr><td>CNPJ</td><td>23**********31</td><td>14 digits</td></tr><tr><td>Phone</td><td>+5511987654321<br>or<br>11987654321</td><td>country code (+55) is optional</td></tr><tr><td>Email</td><td>merchant@pagsmile.com</td><td></td></tr><tr><td>EVP</td><td>A UUID-like string: a1073db4-a3a0-11ed-a8fc-0242ac120002</td><td>alphanumeric string of 32 digits that is sent from the central bank to the institution</td></tr></tbody></table>
