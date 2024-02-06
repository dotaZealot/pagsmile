---
description: Required for Some Cash and Banktransfer methods
---

# Supported Bank List Query

{% hint style="info" %}
This API is only used for Brazil (OpenFinance), Chile (Khipu), Argentina, Bolivia, Paraguay and Uruguay
{% endhint %}

#### Request Base URL <a href="#request-base-url" id="request-base-url"></a>

```
  Test Environment : https://gateway-test.pagsmile.com
  Prod Environment : https://gateway.pagsmile.com
```

#### EndPoints <a href="#endpoints" id="endpoints"></a>

```
  /trade/bank-list
```

#### Request Header <a href="#request-header" id="request-header"></a>

| Parameter     | Required  | Description                         |
| ------------- | --------- | ----------------------------------- |
| Content-Type  | recommend | application/json                    |
| Authorization | yes       | Basic Base64(app\_id:security\_key) |

#### Request Body (JSON format) <a href="#request-body-json-format" id="request-body-json-format"></a>

| Parameter | Type   | Required | Max Length(or Default Value) | Description                                                                                          |
| --------- | ------ | -------- | ---------------------------- | ---------------------------------------------------------------------------------------------------- |
| app\_id   | string | yes      | 32                           | created app's id at dashboard                                                                        |
| timestamp | string | yes      | 19                           | yyyy-MM-dd HH:mm:ss                                                                                  |
| method    | string | yes      | 32                           | [Supported Method（Cash、BankTransfer、Khipu）](https://developer.pagsmile.com/en/reference/method-list) |

#### Request Sample <a href="#request-sample" id="request-sample"></a>

```
curl --location --request POST 'https://gateway.pagsmile.com/trade/bank-list' \
--header 'Authorization: Basic Base64(appid:secret_key)' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "app_id",
    "timestamp": "{{datetime}}",
    "method": "{{method}}"
}'
```

#### Http Response (JSON format) <a href="#http-response-json-format" id="http-response-json-format"></a>

| Parameter       | Type   | Description                                  |
| --------------- | ------ | -------------------------------------------- |
| code            | string | return code                                  |
| msg             | string | return message                               |
| data.bank\_id   | string | bank id: used for parameter "bank"           |
| data.bank\_name | string | bank name                                    |
| min\_amount     | string | min amount for this bank. **Only for Khipu** |
| data.detail     | string |                                              |

#### Return Code (Success) <a href="#return-code-success" id="return-code-success"></a>

```
{
    "code": "10000",
    "msg": "Success",
    "data"."bank_id": "{{bank_id}}",
    "data"."bank_name": "{{bank_name}}",
    "min_amount": "200",
    "data"."detail": ""
}
```

#### Return Code (Fail) <a href="#return-code-fail" id="return-code-fail"></a>

```
{
    "code": "40002",
    "msg": "Business Failed",
    "sub_code": "invalid-signature",
    "sub_msg": "invalid signature"
}
```
