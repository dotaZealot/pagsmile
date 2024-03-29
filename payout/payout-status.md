# Payout Status

{% swagger baseUrl="https://sandbox.transfersmile.com" path="/api/payout/status" method="post" summary="Get Payout Status" %}
{% swagger-description %}
This endpoint allows you to get payout status.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" type="string" required="true" %}
Get AppId from dashboard
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
signature, generated by SHA256($sorted\_params + $app\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="payout_id" type="string" %}
pagsmile transaction id, payout\_id or custom\_code required.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" type="string" %}
merchant custom\_code, payout\_id or custom\_code required.
{% endswagger-parameter %}

{% swagger-response status="200" description="success " %}
```
{
    "code": 200,
    "msg": "success",
    "time": 1628497163,
    "data": {
        "payout_id": "TPO2108090705014iNqtxektRS",
        "custom_code": "custom_code17902976588800",
        "status": "PAID",
        "description": "success"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="custom_code or payout_id required" %}
```
{
    "code": 400,
    "msg": "invalid parameters",
    "time": 1628497751,
    "data": {
        "error": "custom_code or payout_id required"
    }
}
```
{% endswagger-response %}

{% swagger-response status="500" description="system error" %}
```
{
    "code": 500,
    "msg": "system error",
    "time": 1628497751,
    "data": {
        "error": "system error"
    }
}
```
{% endswagger-response %}
{% endswagger %}

## Payout Status

| Status         | Description                      |
| -------------- | -------------------------------- |
| IN\_PROCESSING | initial status after submitting. |
| PROCESSING     | bank processing                  |
| PAID           | payout finished successfully     |
| REJECTED       | payout rejected by bank          |
| REFUNDED       | payout refunded by bank          |

{% hint style="info" %}
_**The Refund of Payout can be issued by the user or by the recipient's bank. Pagsmile cannot issue a refund of the PAID transactions.**_
{% endhint %}

## Example

```
curl --location --request POST 'https://sandbox.transfersmile.com/api/payout/status' \
--header 'AppId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
    "payout_id": "TPO2108090705014iNqtxektRS",
    "custom_code": "custom_code17902976588800"
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is pagsmile's test merchant id for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}
