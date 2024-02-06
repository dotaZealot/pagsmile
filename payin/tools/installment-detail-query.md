# Installment Detail Query



#### Request Base URL <a href="#request-base-url" id="request-base-url"></a>

```
  Test Environment : https://gateway-test.pagsmile.com
  Prod Environment : https://gateway.pagsmile.com
```

#### EndPoints <a href="#endpoints" id="endpoints"></a>

```
  /trade/installments
```

#### Request Header <a href="#request-header" id="request-header"></a>

| Parameter     | Required  | Description                         |
| ------------- | --------- | ----------------------------------- |
| Content-Type  | recommend | application/json                    |
| Authorization | yes       | Basic Base64(app\_id:security\_key) |

#### Request Body (JSON format) <a href="#request-body-json-format" id="request-body-json-format"></a>

| Parameter | Type    | Required | Max Length(or Default Value) | Description                   |
| --------- | ------- | -------- | ---------------------------- | ----------------------------- |
| app\_id   | string  | yes      | 32                           | created app's id at dashboard |
| timestamp | string  | yes      | 19                           | yyyy-MM-dd HH:mm:ss           |
| amount    | decimal | yes      | 0.01 \~ 99999999999999.99    | amount                        |
| currency  | string  | yes      | 3                            | currency                      |

#### Request Sample <a href="#request-sample" id="request-sample"></a>

```
curl --location --request POST 'https://gateway.pagsmile.com/trade/installments' \
--header 'Authorization: Basic Base64(appid:security_key)' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "app_id",
    "timestamp": "{{datetime}}",
    "amount": "{{amount}}",
    "currency": "{{currency}}"
}'
```

#### Http Response (JSON format) <a href="#http-response-json-format" id="http-response-json-format"></a>

| Parameter | Type                                                                                | Description     |
| --------- | ----------------------------------------------------------------------------------- | --------------- |
| code      | string                                                                              | return code     |
| msg       | string                                                                              | return msg      |
| fee       | List [Fee](https://developer.pagsmile.com/en/reference/installments-query.html#Fee) | fee detail list |

**Fee**

| Parameter    | Type   | Description           |
| ------------ | ------ | --------------------- |
| stage        | string | stage of installments |
| amount\_each | string | amount for each stage |
| amount       | Fee    | total amount          |

#### Return Code (Success) <a href="#return-code-success" id="return-code-success"></a>

```
{
    "code": "10000",
    "msg": "Success",
    "fee": [
      {
        "stage":1,
        "amount_each":200.00,
        "amount":200.00
      },
      ...
    ]
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
