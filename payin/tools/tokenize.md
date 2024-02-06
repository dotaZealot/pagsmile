# Get CreditCard Token

#### Request Base URL <a href="#request-base-url" id="request-base-url"></a>

```
  Test Environment : https://security-test.pagsmile.com
  Prod Environment : https://security.pagsmile.com
```

#### EndPoints <a href="#endpoints" id="endpoints"></a>

```
  /card/token
```

#### Request Header <a href="#request-header" id="request-header"></a>

| Parameter     | Required  | Description                         |
| ------------- | --------- | ----------------------------------- |
| Content-Type  | recommend | application/json                    |
| Authorization | yes       | Basic Base64(app\_id:security\_key) |

#### Request Body (JSON format) <a href="#request-body-json-format" id="request-body-json-format"></a>

| Parameter                         | Type   | Required | Max Length(or Default Value) | Description                   |
| --------------------------------- | ------ | -------- | ---------------------------- | ----------------------------- |
| app\_id                           | string | yes      | 32                           | created app's id at dashboard |
| timestamp                         | string | yes      | 19                           | yyyy-MM-dd HH:mm:ss           |
| card.card\_no                     | string | yes      | 32                           |                               |
| card.issuer                       | string | yes      | 16                           | visa,mastercard...            |
| card.holder.name                  | string | yes      | 64                           |                               |
| card.holder.identification.type   | string | no       | 16                           |                               |
| card.holder.identification.number | string | yes      | 64                           |                               |
| card.cvv                          | string | yes      | 8                            | security code                 |
| card.valid\_thru\_year            | string | yes      | 4                            | expire year                   |
| card.valid\_thru\_month           | string | yes      | 2                            | expire month                  |

#### Request Sample <a href="#request-sample" id="request-sample"></a>

```
curl --location --request POST 'https://security.pagsmile.com/card/token' \
--header 'Authorization: Basic Base64(appid:security_key)' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "app_id",
    "timestamp": "{{datetime}}",
    "card": {
      "card_no": "card_no",
      ...
    }
}'
```

#### Http Response (JSON format) <a href="#http-response-json-format" id="http-response-json-format"></a>

| Parameter | Type   | Description                 |
| --------- | ------ | --------------------------- |
| code      | string | return code                 |
| msg       | string | return msg                  |
| sub\_code | string | return sub code(only error) |
| sub\_msg  | string | return sub msg(only error)  |
| token     | string |                             |

#### Return Code (Success) <a href="#return-code-success" id="return-code-success"></a>

```
{
    "code": "10000",
    "msg": "Success",
    "token": "{token}",
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
