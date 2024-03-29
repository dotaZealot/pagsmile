---
description: How to get your payout detail list.
---

# Payout List

{% swagger baseUrl="https://sandbox.transfersmile.com" path="/api/payout/list" method="post" summary="This endpoint allows you to get payout list." %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" type="string" required="true" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
signature, generated by SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="start_time" type="string" required="true" %}
start\_time(UTC), e.g. 2021-07-01 00:00:00
{% endswagger-parameter %}

{% swagger-parameter in="body" name="end_time" type="string" required="true" %}
end\_time(UTC), e.g. 2021-08-01 00:00:00
{% endswagger-parameter %}

{% swagger-parameter required="true" in="body" name="page_num" type="integer" %}
paging param, page number, should start from  _**1**_, while _**0**_ is **incorrect**.
{% endswagger-parameter %}

{% swagger-parameter required="true" in="body" name="page_size" type="integer" %}
paging param, rows will be returned, default 0, max 1000
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" type="integer" required="true" %}
unix timestamp, e.g. 1628512575
{% endswagger-parameter %}

{% swagger-response status="200" description="Payout list successfully retrieved." %}
```
{
    "code": 200,
    "msg": "success",
    "time": 1628500091,
    "data": [
        {
            "reference_id": "custom_codexxxx",
            "transaction_id": "TS202108090705014iNqtxektRS",
            "user_name": "GUILHERME ALVES DE SOUZA",
            "bank_id": "EXXXXD", // only supported by pix payout.
            "amount": "0.6",
            "source_amount": "0.6",
            "settlement_amount": "0.6",
            "source_currency": "BRL",
            "arrival_amount": "0.57",
            "arrival_currency": "BRL",
            "exchange_rate": "1",
            "tax": "0.02",
            "fee": "0.01",
            "fee_user": "beneficiary",
            "transaction_status": "PROCESSING",
            "create_time": 1625142259,
            "update_time": 1625142261
        },
        ... ...
    ]
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
curl --location --request POST 'https://sandbox.transfersmile.com/api/payout/list' \
--header 'AppId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
   * "start_time": "2021-07-01 00:00:00",
   * "end_time": "2021-08-01 00:00:00",
   * "page_size": 5, // should be greater than 0
   * "page_num": 1, // should start from the number 1, while 0 is incorrect.
   * "timestamp": 1628512575
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is pagsmile's test merchant id for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

{% hint style="danger" %}
Note: The _**page\_num**_ should start from the number 1, while 0 is incorrect. The _**page\_size**_ should be greater than 0.
{% endhint %}
