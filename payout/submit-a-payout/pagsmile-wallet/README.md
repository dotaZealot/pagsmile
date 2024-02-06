---
description: How to use Pagsmile Wallet to submit a payout.
coverY: 0
---

# Pagsmile Wallet

{% content-ref url="h5-authorization.md" %}
[h5-authorization.md](h5-authorization.md)
{% endcontent-ref %}

{% content-ref url="native-app-authorization.md" %}
[native-app-authorization.md](native-app-authorization.md)
{% endcontent-ref %}

{% content-ref url="send-prizes.md" %}
[send-prizes.md](send-prizes.md)
{% endcontent-ref %}

## Environment

<table><thead><tr><th width="178.33365608328495">Environment</th><th>API</th></tr></thead><tbody><tr><td>sandbox</td><td>https://sandbox.transfersmile.com/api/payout</td></tr><tr><td>product</td><td>https://api.transfersmile.com/api/payout</td></tr></tbody></table>

## HTTP Method

POST

## HTTP Header

<table><thead><tr><th width="150">Header</th><th width="150">Type</th><th width="150">Required</th><th>Description</th></tr></thead><tbody><tr><td>Content-Type</td><td>String</td><td>Yes</td><td>application/json; charset=UTF-8</td></tr><tr><td>AppId</td><td>String</td><td>Yes</td><td>Your App ID in payout platform</td></tr><tr><td>Authorization</td><td>String</td><td>Yes</td><td>SHA256($sorted_params + $app_key)</td></tr></tbody></table>

## HTTP Body(Only JSON Supported)

<table><thead><tr><th width="161.4068079857687">Parameter</th><th width="156.44870898216672">Type</th><th width="168.02484649863064">Required</th><th>Description</th></tr></thead><tbody><tr><td>name</td><td>String</td><td>No</td><td><p>Beneficiary's name</p><p>Min.5 Max.100 </p></td></tr><tr><td>phone</td><td>String</td><td>No</td><td><p>Beneficiary's phone</p><p>- Max.15 -</p></td></tr><tr><td>email</td><td>String</td><td>No</td><td>Beneficiary's email</td></tr><tr><td>account</td><td>String</td><td>Yes</td><td>Pagsmile Wallet account</td></tr><tr><td>account_type</td><td>String</td><td>Yes</td><td>Fixed Value: UUID</td></tr><tr><td>method</td><td>String</td><td>Yes</td><td>Fixed Value: WALLET</td></tr><tr><td>channel</td><td>String</td><td>Yes</td><td>Fixed Value: Pagsmile</td></tr><tr><td>amount</td><td>Numeric String</td><td>Yes</td><td><p>Payout amount</p><p>- Min 0.01, Max 50,000 -</p></td></tr><tr><td>amount_type</td><td>String</td><td>No</td><td><p>Specify the amount value is fixed for merchant or beneficiary:</p><p>source_amount, arrival_amount(default) </p></td></tr><tr><td>fee_bear</td><td>String</td><td>Yes</td><td>One of [beneficiary | merchant]</td></tr><tr><td>custom_code</td><td>String</td><td>Yes</td><td><p>Merchant's order id</p><p>- Max.50 -</p></td></tr><tr><td>source_currency</td><td>String</td><td>Yes</td><td>Merchant's account currency, supported: USD, GBP, EUR</td></tr><tr><td>arrival_currency</td><td>String</td><td>Yes</td><td>Beneficiary's account currency, BRL or MXN</td></tr><tr><td>notify_url</td><td>String</td><td>Yes</td><td>Where pagsmile will callback to</td></tr><tr><td>additional_remark</td><td>String</td><td>Yes</td><td>Payout Additional Remark, Max length: 40 </td></tr><tr><td>country</td><td>String</td><td>Yes</td><td>Country code, BRA or MEX</td></tr></tbody></table>

## Request Example

```
// test demo by curl
curl --location --request POST 'https://sandbox.transfersmile.com/api/payout' \
--header 'AppId: 94FAC**********************68548' \
--header 'Authorization: d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302' \
--header 'Content-Type: application/json' \
--data-raw '{
      "name": "Alan **** **** Santana",
      "email": "pagsmile_wallet_demo@pagsmile.com",
    * "account": "f341************************0844",
    * "account_type": "UUID",
    * "amount": "10.00",
    * "source_currency": "USD",
    * "arrival_currency": "BRL",
    * "custom_code": "custom_code_pwallet_10010", // merchant order id
    * "fee_bear": "merchant",
    * "method": "WALLET",
    * "channel": "Pagsmile",
    * "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    * "additional_remark": "Pagsmaile wallet test",
    * "country": "BRA"
}'
```

{% hint style="info" %}
Note:  _**94FAC\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*68548**_ is pagsmile's test App ID for sandbox, and _**d6181db0d6548b94b162e75d095b59147172d914699f83b2bd17951a671b6302**_ is authorization token associated with the test App ID.
{% endhint %}

## HTTP Response

```
// success
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "TS202108100734054iRiUZFPXfQWB", // pagsmile payout id
        "custom_code": "custom_code9982674851738108", // merchant order id
        "arrival_amount": "100",
        "arrival_currency": "BRL",
        "source_amount": "0.07",
        "source_currency": "USD",
        "status": "IN_PROCESSING"
    }
}
```

```
// bad request
{
    "code": 4001000,
    "msg": "invalid parameter",
    "time": 1637224716,
    "data": {
        ... ...
    }
}
```

```
// persmission denied
{
    "code": 4004003,
    "msg": "permission denied",
    "time": 1637224716,
    "data": {
        ... ...
    }
}
```

```
// balance insufficient
{
    "code": 5001102,
    "msg": "balance insufficient",
    "time": 1637224716,
    "data": {
        ... ...
    }
}
```

```
// system error
{
    "code": 5001000,
    "msg": "system error",
    "time": 1637224716,
    "data": {
        ... ...
    }
}
```

## Supported Countries

| Country | Country Code | Currency |
| ------- | ------------ | -------- |
| Brazil  | BRA          | BRL      |
| Mexico  | MEX          | MXN      |

