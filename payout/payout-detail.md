# Payout Detail

{% swagger baseUrl="https://sandbox.transfersmile.com" path="/api/payout/detail" method="post" summary="Get Payout Detail" %}
{% swagger-description %}
This endpoint allow you get payout detail.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" type="string" required="true" %}
Get App ID from dashboard.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="transaction_id" type="string" required="true" %}
Pagsmile transaction id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" type="integer" required="true" %}
unix timestamp, e.g. 1628512575
{% endswagger-parameter %}

{% swagger-response status="200" description="Payout detail successfully retrieved" %}
```
{
    "code": 200,
    "msg": "success",
    "time": 1628569551,
    "data": {
        "reference_id": "custom_codexxxx",
        "transaction_id": "TS202108090705014iNqtxektRS",
        "user_name": "GUILHERME ALVES DE SOUZA",
        "bank_id": "EXXXXD", // only supported by pix payout.
        "amount": "0.55",
        "source_amount": "3.58",
        "settlement_amount": "0.55",
        "source_currency": "BRL",
        "arrival_amount": "0.55",
        "arrival_currency": "BRL",
        "exchange_rate": "1",
        "tax": "0.02",
        "fee": "3.01",
        "fee_user": "merchant",
        "transaction_status": "PAID",
        "create_time": 1628492701,
        "update_time": 1628495767
    }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Request has expired" %}
```
{
    "code": 4001009,
    "msg": "request has expired",
    "time": 1628512773,
    "data": {}
}
```
{% endswagger-response %}
{% endswagger %}

## Example

```
curl --location --request POST 'https://sandbox.transfersmile.com/api/payout/detail' \
--header 'AppId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
    "transaction_id": "TPO2108090705014iNqtxektRS",
    "timestamp": 1628569550
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is pagsmile's test merchant id for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}
