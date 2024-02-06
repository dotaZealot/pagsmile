---
description: How to use Bank Transfer to submit a payout in Turkey.
---

# BankTransfer

{% swagger method="post" path="/api/payout" baseUrl="https://sandbox.transfersmile.com " summary="Submit a payout by Bank Transfer in Turkey" %}
{% swagger-description %}
This endpoint allows you to submit a payout by Bank Transfer in Trazil.
{% endswagger-description %}

{% swagger-parameter in="header" required="true" name="Content-Type" type="string" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" type="string" name="AppId" %}
Your App ID in payout platform.
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" type="string" name="Authorization" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" required="true" name="name" type="string" %}
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

{% swagger-parameter in="body" name="document_id" type="string" %}
Beneficiary's personal identification number.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_type" type="string" %}
Beneficiary's personal identification type

\- Fixed Value: NIN -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" type="string" required="true" %}
Beneficiary's Bank Account

\- TR + 24 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_type" type="string" required="true" %}
Beneficiary's Account Type\
\- Fixed Value: IBAN -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" required="true" %}
Fixed value: BANKTRANSFER
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="custom_code" required="true" %}
Merchant Payout ID\
\- Max. 50 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" type="string" required="true" %}
Processing fee charges to merchant or beneficiary\
\- One of: merchant, beneficiary -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="number" required="true" %}
Payout Amount, 2 decimal numbers

\- Min 0.01, Max 500,000 -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount_type" type="string" required="false" %}
Specify the amount value is fixed for merchant or beneficiary\
\- One of: source\_amount, arrival\_amount(default) -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" type="string" required="true" %}
Merchant Account Currency\
\- One of: USD, EUR, GBP, TRY -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" type="string" required="true" %}
Fixed value: TRY
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where pagsmile will send notification to.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="addtional_remark" type="string" required="true" %}
Descriptor on the user's bank bill\
\- Max. 40 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" type="string" required="true" %}
Fixed Valud: TUR, for Turkey
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
```
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
```
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
```
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
```
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
    * "name": "GUILHERME ****** SOUZA",
      "phone": "",
      "email": "payout@pagsmile.com",
    * "amount": "10.01",
    * "arrival_currency": "TRY", // fixed value: TRY
    * "custom_code" : "custom_code_your_order_id",
      "document_id": "22*******99",
      "document_type": "NIN",
    * "fee_bear": "merchant",
    * "method": "BankTransfer",   // fixed value: BankTransfer
    * "notify_url": "https://notify.url",
    * "account": "TR112233445566778899001122", // TR + 24 digits
    * "account_type": "IBAN",  // fixed value: IBAN
    * "source_currency": "USD", // supported: USD GBP EUR TRY
    * "additional_remark": "pagsmile payout test remark",
    * "country": "TUR", // fixed value: TUR
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is Pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

## Example of Document

| Document Type | Document ID        | Description |
| ------------- | ------------------ | ----------- |
| NIN           | 22\*\*\*\*\*\*\*99 | 11 digits   |

## Example of BankTransfer Account

| Account Type | Account                    | Description                                                                         |
| ------------ | -------------------------- | ----------------------------------------------------------------------------------- |
| IBAN         | TR112233445566778899001122 | TR + 2 Check digits + 5 Bank code + 1 National check digit + 16 bank account number |
