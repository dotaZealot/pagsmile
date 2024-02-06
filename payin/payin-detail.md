# Payin Detail



#### Request Base URL <a href="#request-base-url" id="request-base-url"></a>

```
  Test Environment : https://gateway-test.pagsmile.com
  Prod Environment : https://gateway.pagsmile.com
```

#### EndPoints <a href="#endpoints" id="endpoints"></a>

```
  /trade/query
```

#### Request Header <a href="#request-header" id="request-header"></a>

| Parameter     | Required  | Description                         |
| ------------- | --------- | ----------------------------------- |
| Content-Type  | recommend | application/json                    |
| Authorization | yes       | Basic Base64(app\_id:security\_key) |

#### Request Body (JSON format) <a href="#request-body-json-format" id="request-body-json-format"></a>

| Parameter      | Type   | Required | Max Length(or Default Value) | Description                                                          |
| -------------- | ------ | -------- | ---------------------------- | -------------------------------------------------------------------- |
| app\_id        | string | yes      | 32                           | created app's id at dashboard                                        |
| timestamp      | string | yes      | 19                           | yyyy-MM-dd HH:mm:ss                                                  |
| out\_trade\_no | string | yes      | 64                           | Merchant's trade NO.(cannot be empty with trade\_no at same time)    |
| trade\_no      | string | yes      | 64                           | Pagsmile trade NO.(cannot be empty with out\_trade\_no at same time) |

#### Request Sample <a href="#request-sample" id="request-sample"></a>

```
curl --location --request POST 'https://gateway.pagsmile.com/trade/query' \
--header 'Authorization: Basic Base64(appid:security_key)' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "app_id",
    "timestamp": "{{datetime}}",
    "out_trade_no": "{{out_trade_no}}",
    "trade_no": "{{trade_no}}"
}'
```

#### Http Response (JSON format) <a href="#http-response-json-format" id="http-response-json-format"></a>

| Parameter                | Type    | Description               |
| ------------------------ | ------- | ------------------------- |
| code                     | string  | return code               |
| msg                      | string  | return msg                |
| out\_trade\_no           | string  | merchant's trade NO.      |
| trade\_no                | string  | Pagsmile's trade NO.      |
| trade\_status            | string  | status                    |
| order\_amount            | decimal | amount                    |
| order\_currency          | string  | currency                  |
| create\_time             | string  | yyyy-MM-dd HH:mm:ss\[UTC] |
| update\_time             | string  | yyyy-MM-dd HH:mm:ss\[UTC] |
| refuse\_detail           | string  | Refuse only               |
| customer.identify.type   | string  |                           |
| customer.identify.number | string  |                           |
| customer.email           | string  |                           |
| customer.phone           | string  |                           |

#### Return Code (Success) <a href="#return-code-success" id="return-code-success"></a>

```
{
    "code": "10000",
    "msg": "Success",
    "trade_no": "",
    "out_trade_no": "",
    "trade_status": "",
    "order_currency": "",
    "order_amount": "",
    "customer": {
        "identify": {
            "number": "",
            "type": ""
        },
        "email": "",
        "phone": ""
    },
    "refuse_detail": "",
    "create_time": "",
    "update_time": ""
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
