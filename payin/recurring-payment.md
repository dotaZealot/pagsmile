# Recurring Payment

## Recurring Payment

#### Request Base URL <a href="#request-base-url" id="request-base-url"></a>

```
  Test Environment : https://gateway-test.pagsmile.com
  Prod Environment : https://gateway.pagsmile.com
```

#### EndPoints <a href="#endpoints" id="endpoints"></a>

```
  /trade/recurring
```

#### Request Header <a href="#request-header" id="request-header"></a>

| Parameter     | Required    | Description                         |
| ------------- | ----------- | ----------------------------------- |
| Content-Type  | Recommended | application/json                    |
| Authorization | Yes         | Basic Base64(app\_id:security\_key) |

#### Request Parameters (JSON format) <a href="#request-parameters-json-format" id="request-parameters-json-format"></a>

| Parameter        | Type    | Required  | Max Length(or Default Value) | Description                                           |
| ---------------- | ------- | --------- | ---------------------------- | ----------------------------------------------------- |
| app\_id          | string  | yes       | 32                           | App's ID is in dashboard                              |
| out\_trade\_no   | string  | yes       | 64                           | Given by the Merchant (Is in their system)            |
| method           | string  | no        | 32                           | Credit Card                                           |
| order\_currency  | string  | yes       | 3                            | BRL for Brazil                                        |
| order\_amount    | decimal | yes       | 0.01 \~ 99999999999999.99    | Request payment amount                                |
| subject          | string  | yes       | 128                          | Payment reason or item title                          |
| content          | string  | no        | 255                          | Payment reason detail or item detail                  |
| trade\_type      | string  | yes       | WEB                          | Response content type, WEB will return a checkout URL |
| timeout\_express | string  | no        | 90m                          | m(minutes), h(hours), d(days), c(current day)         |
| format           | string  | no        | JSON                         | Only JSON supported                                   |
| timestamp        | string  | yes       | 19                           | yyyy-MM-dd HH:mm:ss                                   |
| version          | string  | yes       | 2.0                          | Fix to 2.0                                            |
| notify\_url      | string  | yes       |                              | IPN URL to merchant (start with http)                 |
| return\_url      | string  | no        |                              | Web page return URL to merchant (start with http)     |
| buyer\_id        | string  | recommend |                              | Merchant user's ID                                    |
| interval         | string  | yes       | 1M                           | D(day), W(week), M(month), Y(year)                    |
| quantity         | number  | no        | 0                            | Quantity of recurring                                 |
| trial\_period    | string  | no        |                              | Trial period                                          |
| trial\_amount    | decimal | no        | > 0                          | Trial amount (when trial\_amount is not blank)        |

#### Request Sample <a href="#request-sample" id="request-sample"></a>

```
curl --location --request POST 'https://gateway.pagsmile.com/trade/recurring' \
--header 'Authorization: Basic Base64(appid:security_key)' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "app_id",
    "content": "content",
    "method": "CreditCard",
    "notify_url": "notify_url",
    "order_amount": 10,
    "order_currency": "BRL",
    "out_trade_no": "{{$randomUUID}}",
    "subject": "subject",
    "timeout_express": "1h",
    "timestamp": "{{datetime}}",
    "trade_type": "WEB",
    "version": "2.0",
    "interval": "1M"
}'
```

#### Http Response (JSON format) <a href="#http-response-json-format" id="http-response-json-format"></a>

| Parameter      | Type   | Description                  |
| -------------- | ------ | ---------------------------- |
| code           | string | Return code                  |
| msg            | string | Return msg                   |
| sub\_code      | string | Return sub code (only error) |
| sub\_msg       | string | Return sub msg (only error)  |
| out\_trade\_no | string | Request out\_trade\_no       |
| trade\_no      | string | Pagsmile trade NO.           |
| web\_url       | string | Checkout URL                 |

#### Return Code (Success) <a href="#return-code-success" id="return-code-success"></a>

```
{
    "code": "10000",
    "msg": "Success",
    "out_trade_no": "{out_trade_no}",
    "trade_no": "{trade_no}",
    "web_url": "http://checkout.pagsmile.com?prepay_id={$prepay_id}",
    "prepay_id": "{$prepay_id}"
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

#### IPN Notifications <a href="#ipn-notifications" id="ipn-notifications"></a>

Follow the [general IPN notifications guide](notification/) to receive our IPN notification messages, meantime with recurring sub orders, we will also send the parameter `period` to specific current period of the order.

```
Content-Type: application/json
Method: POST
Header: Pagsmile-Signature
Body:
  {
  	"amount":"",
  	"out_trade_no":"",
  	"method":"",
  	"trade_status":"",
  	"trade_no":"",
  	"currency":"",
  	"out_request_no":"",
  	"app_id":"",
    "timestamp":"",
    "user":{
      "identify":{
        "number":"",
        "type":""
      },
      "phone":"",
      "email":""
    },
    "card":{
      "card_no":"F6L4"
    },
    "period": 1
  }
```

#### Attention!!! <a href="#attention" id="attention"></a>

return\_url is not in the request parameters, if needed, just append the return\_url after the web\_url when redirect:

http://checkout.pagsmile.com?prepay\_id={$prepay\_id}

## Cancel Recurring Payment&#x20;



#### Request Base URL <a href="#request-base-url" id="request-base-url"></a>

```
  Test Environment : https://gateway-test.pagsmile.com
  Prod Environment : https://gateway.pagsmile.com
```

#### EndPoints <a href="#endpoints" id="endpoints"></a>

```
  /trade/recurring/cancel
```

#### Request Header <a href="#request-header" id="request-header"></a>

| Parameter     | Required    | Description                         |
| ------------- | ----------- | ----------------------------------- |
| Content-Type  | Recommended | application/json                    |
| Authorization | Yes         | Basic Base64(app\_id:security\_key) |

#### Request Parameters (JSON format) <a href="#request-parameters-json-format" id="request-parameters-json-format"></a>

| Parameter      | Type   | Required | Max Length(or Default Value) | Description                                |
| -------------- | ------ | -------- | ---------------------------- | ------------------------------------------ |
| app\_id        | string | yes      | 32                           | App's ID is in dashboard                   |
| timestamp      | string | yes      | 19                           | yyyy-mm-dd HH:mm:ss                        |
| version        | string | yes      | 2.0                          | fix to 2.0                                 |
| out\_trade\_no | string | yes      | 64                           | Given by the Merchant (Is in their system) |

#### Request Sample <a href="#request-sample" id="request-sample"></a>

```
curl --location --request POST 'https://gateway.pagsmile.com/trade/recurring/cancel' \
--header 'Authorization: Basic Base64(appid:security_key)' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "app_id",
    "timestamp": "{{datetime}}",
    "version": "2.0",
    "out_trade_no": "{{$randomUUID}}"
}'
```

#### Http Response (JSON format) <a href="#http-response-json-format" id="http-response-json-format"></a>

| Parameter         | Type   | Description                 |
| ----------------- | ------ | --------------------------- |
| code              | string | Return code                 |
| msg               | string | Return msg                  |
| sub\_code         | string | Return sub code(only error) |
| sub\_msg          | string | Return sub msg(only error)  |
| out\_trade\_no    | string | Request out\_trade\_no      |
| recurring\_status | string | Recurring status            |

#### Return Code (Success) <a href="#return-code-success" id="return-code-success"></a>

```
{
    "code": "10000",
    "msg": "Success",
    "out_trade_no": "{out_trade_no}",
    "recurring_status": "CANCEL"
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
