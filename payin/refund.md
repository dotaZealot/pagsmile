# Refund

<table><thead><tr><th>Method</th><th width="287">Refund Type</th><th>Require User Info</th></tr></thead><tbody><tr><td>Pix</td><td>Refund through banktransfer</td><td>Required</td></tr><tr><td>Boleto</td><td>Refund through banktransfer</td><td>Required</td></tr><tr><td>Lottery</td><td>Refund through banktransfer</td><td>Required</td></tr><tr><td>Deposit Express</td><td>Refund through banktransfer</td><td>Required</td></tr><tr><td>SPEI</td><td>Refund through banktransfer</td><td>Required</td></tr><tr><td>Wallet</td><td>Refund through original source</td><td>Not Required</td></tr><tr><td>CreditCard</td><td>Refund through original source</td><td>Not Required</td></tr></tbody></table>

#### Request Base URL <a href="#request-base-url" id="request-base-url"></a>

```
  Test Environment : https://gateway-test.pagsmile.com
  Prod Environment : https://gateway.pagsmile.com
```

#### EndPoints <a href="#endpoints" id="endpoints"></a>

```
  /trade/refund
```

#### Request Header <a href="#request-header" id="request-header"></a>

| Parameter     | Required    | Description                         |
| ------------- | ----------- | ----------------------------------- |
| Content-Type  | Recommended | Application/json                    |
| Authorization | Yes         | Basic Base64(app\_id:security\_key) |

#### Request Body (JSON format) <a href="#request-body-json-format" id="request-body-json-format"></a>

| Parameter                  | Type    | Required | Max Length(or Default Value) | Description                                                                             |
| -------------------------- | ------- | -------- | ---------------------------- | --------------------------------------------------------------------------------------- |
| app\_id                    | string  | yes      | 32                           | App's ID is in dashboard                                                                |
| timestamp                  | string  | yes      | 19                           | yyyy-MM-dd HH:mm:ss                                                                     |
| trade\_no                  | string  | yes      | 64                           | Pagsmile trade NO.(can NOT be empty with out\_trade\_no at same time)                   |
| out\_trade\_no             | string  | yes      | 64                           | ID given by the merchant in their system (can NOT be empty with trade\_no at same time) |
| out\_request\_no           | string  | no       | 16                           | refund request unique NO.(can NOT be empty when request a partial refund)               |
| refund\_currency           | string  | yes      | 3                            |                                                                                         |
| refund\_amount             | decimal | yes      | 0.01 \~ 99999999999999.99    |                                                                                         |
| refund\_reason             | string  | no       | 128                          |                                                                                         |
| user\_info.identify.number | string  | yes      | 16                           | User ID                                                                                 |
| user\_info.identify.type   | string  | no       | 16                           | User's ID type                                                                          |
| user\_info.name            | string  | yes      | 64                           | User's name                                                                             |
| user\_info.email           | string  | yes      | 64                           | User's email                                                                            |
| user\_info.phone           | string  | no       | 64                           | User's phone                                                                            |
| bank\_info.bank\_id        | string  | no       | 64                           | User's bank ID to receive refund                                                        |
| bank\_info.bank\_name      | string  | no       | 64                           | User's bank name to receive the refund                                                  |
| bank\_info.agency          | string  | no       | 64                           | User's bank agency to receive the refund                                                |
| bank\_info.type            | string  | no       | 64                           | User's bank type to receive the refund                                                  |
| bank\_info.number          | string  | no       | 64                           | User's bank number to receive refund                                                    |

#### Request Sample <a href="#request-sample" id="request-sample"></a>

```
curl --location --request POST 'https://gateway.pagsmile.com/trade/refund' \
--header 'Authorization: Basic Base64(appid:security_key)' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "app_id",
    "content": "content",
    "trade_no": "trade_no",
    "refund_amount": 10,
    "refund_currency": "BRL",
    "out_trade_no": "{{$randomUUID}}",
    "user_info": {
      "identify": {
        "number": "number",
        "type": "type"
      },
      "name": "name",
      "email": "email"
      }
}'
```

#### Http Response (JSON format) <a href="#http-response-json-format" id="http-response-json-format"></a>

| Parameter        | Type    | Description                 |
| ---------------- | ------- | --------------------------- |
| code             | string  | Return code                 |
| msg              | string  | Return msg                  |
| sub\_code        | string  | Return sub code(only error) |
| sub\_msg         | string  | Return sub msg(only error)  |
| out\_trade\_no   | string  |                             |
| trade\_no        | string  |                             |
| refund\_currency | string  |                             |
| refund\_amount   | decimal |                             |
| refund\_status   | string  |                             |

#### Return Sample (Success) <a href="#return-sample-success" id="return-sample-success"></a>

```
{
    "code": "10000",
    "msg": "Success",
    "out_trade_no": "{out_trade_no}",
    "trade_no": "{trade_no}",
    "refund_currency": "{refund_currency}",
    "refund_amount": "{refund_amount}",
    "refund_status": "{refund_status}"
}
```

#### Return Sample (Fail) <a href="#return-sample-fail" id="return-sample-fail"></a>

```
{
    "code": "40002",
    "msg": "Business Failed",
    "sub_code": "invalid-signature",
    "sub_msg": "invalid signature"
}
```
