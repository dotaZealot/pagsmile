---
description: API Direct Payment
---

# Direct integration



#### Request Base URL <a href="#request-base-url" id="request-base-url"></a>

```
  Test Environment : https://gateway-test.pagsmile.com
  Prod Environment : https://gateway.pagsmile.com
```

#### EndPoints <a href="#endpoints" id="endpoints"></a>

```
  /trade/pay
```

#### Request Header <a href="#request-header" id="request-header"></a>

| Parameter     | Required  | Description                         |
| ------------- | --------- | ----------------------------------- |
| Content-Type  | recommend | application/json                    |
| Authorization | yes       | Basic Base64(app\_id:security\_key) |

#### Request Body (JSON format) <a href="#request-body-json-format" id="request-body-json-format"></a>

| Parameter                | Type    | Required | Max Length(or Default Value) | Description                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------ | ------- | -------- | ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| app\_id                  | string  | yes      | 32                           | created app's id at dashboard                                                                                                                                                                                                                                                                                                                                                                  |
| timestamp                | string  | yes      | 19                           | yyyy-MM-dd HH:mm:ss                                                                                                                                                                                                                                                                                                                                                                            |
| out\_trade\_no           | string  | yes      | 64                           | ID given by the merchant in their system                                                                                                                                                                                                                                                                                                                                                       |
| method                   | string  | no       | 32                           | [Payment Methods](https://docs.pagsmile.com/payin/data/payment-method)                                                                                                                                                                                                                                                                                                                         |
| channel                  | string  | no       | 32                           | sub channel(only use at method 'Wallet')                                                                                                                                                                                                                                                                                                                                                       |
| order\_currency          | string  | yes      | 3                            | BRL for brazil                                                                                                                                                                                                                                                                                                                                                                                 |
| order\_amount            | decimal | yes      | 0.01 \~ 99999999999999.99    | request payment amount                                                                                                                                                                                                                                                                                                                                                                         |
| subject                  | string  | yes      | 128                          | payment reason or item title                                                                                                                                                                                                                                                                                                                                                                   |
| content                  | string  | Yes      | 255                          | payment reason detail or item detail. . This will be shown on the bank bill.                                                                                                                                                                                                                                                                                                                   |
| notify\_url              | string  | yes      |                              | IPN URL to merchant(start with http                                                                                                                                                                                                                                                                                                                                                            |
| buyer\_id                | string  | yes      |                              | merchant user's id                                                                                                                                                                                                                                                                                                                                                                             |
| timeout\_express         | string  | no       | 90m                          | m(minutes), h(hours), d(days), c(always end in currency day)                                                                                                                                                                                                                                                                                                                                   |
| token                    | string  | no       |                              | [required for CreditCard](../tools/pagsmile-javascript.md)                                                                                                                                                                                                                                                                                                                                     |
| fingerprint              | string  | no       |                              | [required for CreditCard](../tools/pagsmile-javascript.md)                                                                                                                                                                                                                                                                                                                                     |
| issuer                   | string  | no       |                              | issuer of credit card（required for CreditCard）                                                                                                                                                                                                                                                                                                                                                 |
| installments             | integer | no       | 1                            | installments for CreditCard                                                                                                                                                                                                                                                                                                                                                                    |
| bank                     | string  | no       |                              | <p>bank code, required for </p><p>DepositExpress (itau,santander,bradesco,banco-do-brasil,caixa)<br>Cash (Use bank_id from <a href="../tools/supported-bank-list-query.md">Bank Query</a>);<br>BankTransfer (Use bank_id from<a href="../tools/supported-bank-list-query.md"> Bank Query</a>);<br>Khipu (Use bank_id from <a href="../tools/supported-bank-list-query.md">Bank Query</a>);</p> |
| language\_code           | string  | no       |                              | language code, required for Cash, BankTransfer. (Use language\_code from [Bank query](../tools/supported-bank-list-query.md))                                                                                                                                                                                                                                                                  |
| customer.name            | string  | yes      |                              | user's name                                                                                                                                                                                                                                                                                                                                                                                    |
| customer.email           | string  | yes      |                              | user's email                                                                                                                                                                                                                                                                                                                                                                                   |
| customer.phone           | string  | yes      |                              | user's mobile phone number                                                                                                                                                                                                                                                                                                                                                                     |
| customer.identify.number | string  | yes      |                              | user's ID number                                                                                                                                                                                                                                                                                                                                                                               |
| customer.identify.type   | string  | yes      |                              | user's ID type                                                                                                                                                                                                                                                                                                                                                                                 |
| address.zip\_code        | string  | yes      |                              | zip code                                                                                                                                                                                                                                                                                                                                                                                       |
| address.state            | string  | yes      |                              | state                                                                                                                                                                                                                                                                                                                                                                                          |
| address.city             | string  | yes      |                              | city                                                                                                                                                                                                                                                                                                                                                                                           |
| address.street\_number   | string  | yes      |                              | street1 number                                                                                                                                                                                                                                                                                                                                                                                 |
| address.street           | string  | yes      |                              | street1                                                                                                                                                                                                                                                                                                                                                                                        |
| address.neighborhood     | string  | no       |                              | street2                                                                                                                                                                                                                                                                                                                                                                                        |
| user\_ip                 | string  | no       |                              | user's IP address(required for CreditCard)                                                                                                                                                                                                                                                                                                                                                     |
| website\_url             | string  | no       | 128                          | merchant website URL                                                                                                                                                                                                                                                                                                                                                                           |

#### Request Sample <a href="#request-sample" id="request-sample"></a>

```
curl --location --request POST 'https://gateway.pagsmile.com/trade/pay' \
--header 'Authorization: Basic Base64(appid:security_key)' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "app_id",
    "content": "content",
    "method": "Boleto",
    "notify_url": "notify_url",
    "order_amount": 10,
    "order_currency": "BRL",
    "out_trade_no": "{{$randomUUID}}",
    "subject": "subject",
    "timeout_express": "1h",
    "timestamp": "{{datetime}}",
    "customer": {
      "name": "name",
      "email": "email",
	  "phone": "phone",
	  "identify": {
		"number":"number",
		"type":"type“，
	  }
      ...
    },
    "address": {
      "zip_code": "84043450",
      "state": "Parana",
      "city": "Ponta Grossa",
      "street"; "Colônia Dona Luíza",
      "street_number": "18",
    },
    "user_ip": "127.0.0.1"
}'
```

#### Http Response (JSON format) <a href="#http-response-json-format" id="http-response-json-format"></a>

<table><thead><tr><th width="191">Parameter</th><th>Type</th><th width="249">Description</th><th width="344">Method</th><th></th></tr></thead><tbody><tr><td>code</td><td>string</td><td>return code</td><td></td><td></td></tr><tr><td>msg</td><td>string</td><td>return msg</td><td></td><td></td></tr><tr><td>sub_code</td><td>string</td><td>return sub code(only error)</td><td></td><td></td></tr><tr><td>sub_msg</td><td>string</td><td>return sub msg(only error)</td><td></td><td></td></tr><tr><td>out_trade_no</td><td>string</td><td>request out_trade_no</td><td></td><td></td></tr><tr><td>trade_no</td><td>string</td><td>Pagsmile trade NO.</td><td></td><td></td></tr><tr><td>trade_status</td><td>string</td><td></td><td></td><td></td></tr><tr><td>pay_url</td><td>string</td><td>Redirect users to the payment URL</td><td><p>Argentina: Khipu, Bank Transfer; </p><p>Brazil: PIX, Lottery, Boleto, DepositExpress; </p><p>Mexico: SPEI, OXXO, OXXOPay;</p><p>Colombia: PSE, Efecty, Bancolombia, SuRed, Wallet ClaroPay, Gana; </p><p>Chile: Khipu, Pago46, Bank Transfer, Cash, Wallet Chek; </p><p>Peru: Bank Transfer, Cash; </p><p>Ecuador: Bank Transfer, Cash; </p><p>Costa Rica: Cash, BNCR; </p><p>Panama, Guatemala: Cash; </p><p>Bolivia, Paraguay, Uruguay: Bank Transfer;</p></td><td></td></tr><tr><td>reference</td><td>string</td><td>The value of reference is the ticket number that the user needs to use for payment</td><td><p>Argentina: Bank Transfer, Rapipago, PagoFacil;</p><p>Mexico: SPEI, CoDi, Cash;</p><p>Colombia: Bancolombia, SuRed, Gana;</p><p>Chile: Cash;</p><p>Peru: Bank Transfer, Cash;</p><p>Costa Rica: Cash, BNCR;</p><p>Panama, Guatemala: Cash;</p><p>Bolivia, Paraguay, Uruguay: Bank Transfer</p></td><td></td></tr><tr><td>barcode</td><td>string</td><td>Use the value of barcode to generate a scanable barcode can help users to make payment faster</td><td><p>Argentina: Rapipago, PagoFacil;</p><p>Brazil: Lottery, Boleto;</p><p>Mexico: OXXO, OXXOPay</p></td><td></td></tr><tr><td>qr_code</td><td>string</td><td>QR code</td><td><p>Brazil: PIX;</p><p>Mexico: CoDi</p></td><td></td></tr><tr><td>qr_code_url</td><td>string</td><td>System generated images of qr code which can be used directly on merchant website depending on needs.</td><td>Brazil: PIX</td><td></td></tr><tr><td>qr_code_img</td><td>string</td><td>System generated images of qr code which can be used directly on merchant website depending on needs.</td><td>Brazil: PIX</td><td></td></tr><tr><td>provider_owner</td><td>string</td><td>bank info : account owner; only in DepositExpress</td><td></td><td></td></tr><tr><td>provider_owner_document</td><td>string</td><td>bank info : account owner document; only in DepositExpress</td><td></td><td></td></tr><tr><td>provider_agency</td><td>string</td><td>bank info : account agency; only in DepositExpress</td><td></td><td></td></tr><tr><td>provider_number</td><td>string</td><td>bank info : account number; only in DepositExpress</td><td></td><td></td></tr><tr><td>partner_code</td><td>string</td><td>The value of reference is the ticket number that the user needs to use for payment</td><td><p>Colombia: Bancolombia, SuRed, Gana;</p><p>Costa Rica: BNCR</p></td><td></td></tr><tr><td>bank_name</td><td>string</td><td>bank info : bank name</td><td><p>Brazil: DepositExpress;</p><p>Mexico: SPEI</p></td><td></td></tr><tr><td>bank_no</td><td>string</td><td>Users only need to use the value of bank_no to finish payment at loterica store</td><td>Brazil: Lottery</td><td></td></tr><tr><td>bank_code</td><td>string</td><td>The ticket number that the user needs to use for payment</td><td>Brazil: Boleto</td><td></td></tr><tr><td>clabe</td><td>string</td><td>Unique automatically generated bank account</td><td>Only SPEI Mexico</td><td></td></tr><tr><td>wallet_url</td><td>string</td><td>Redirect users to the wallet payment page</td><td><p>Only in Wallet payment method Brazil: AME, PicPay;</p><p>Colombia: Wallets (Tpaga, Dale, Daviplata, Movii, Nequi, Rappipay)</p></td><td></td></tr><tr><td>app_link_url</td><td>string</td><td>Redirect users to the wallet app payment page (for mobile walle application)</td><td><p>For mobile wallet app use only Brazil: AME;</p><p>Chile: Mach, Vita</p></td><td></td></tr><tr><td>instruction</td><td>string</td><td>Take the recipient's bank details from the response parameter - "instruction" and present to users</td><td>Bolivia, Paraguay, Uruguay: Bank Transfer</td><td></td></tr></tbody></table>

#### Return Code (Success) <a href="#return-code-success" id="return-code-success"></a>

```
{
    "code": "10000",
    "msg": "Success",
    "out_trade_no": "{out_trade_no}",
    "trade_no": "{trade_no}",
    "trade_status": "PROCESSING",
    "pay_url": "https://checkout-testv2.pagsmile.com/checkout?prepay_id=XX",
    "barcode": "{barcode}",
    "qr_code": "{qr_code}",
    "provider_owner": "{provider_owner}",
    "provider_owner_document": "{provider_owner_document}",
    "provider_agency": "{provider_agency}",
    "provider_number": "{provider_number}",
    "wallet_url": "{wallet_url}",
    "app_link_url": "{app_link_url}"
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

{% hint style="warning" %}
**Attention**

Return\_url is not required in the request parameters, you can also append the return\_url after the web\_url when redirect:

http://checkout.pagsmile.com?prepay\_id={$prepay\_id}

↓↓↓

http://checkout.pagsmile.com?prepay\_id={$prepay\_id}\&return\_url={$return\_url}
{% endhint %}
