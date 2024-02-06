---
description: Notification of virtual account payments
---

# Notification of Virtual Account Payment

{% hint style="info" %}
Notification of virtual account payment follows the same rule as notification of other payment methods. The only difference is the "**transfer\_account**" part. Check [here](../../../notification/) to view the general rules of notification.
{% endhint %}

## Example

```
curl --location --request POST 'http://merchant/callback/success' \\merchant's notify_url
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "amount": "50.00",
    * "out_trade_no": "202201010354002",
    * "method": "SPEI",
    * "trade_status": "SUCCESS",
    * "trade_no": "2022022201111100011",
    * "currency": "MXN",
    * "app_id": "162************38",
    * "user": {
        "buyer_id": "",
    *     "email": "test@pagsmile.com",
    *     "identify": {
    *         "number": "MAMB780915969",
    *         "type": "RFC"
          },
          "ip": "0.0.0.0",
    *     "name": "test user name"
      },
    * "timestamp": "1645516741",
    * "transfer_account": {
    *     "account_id": "DP8F********ME4T",
    *     "account_number": "646************069",
    *     "beneficiary_name": "PAGSMILE MEXICO SA DE CV",
    *     "provider": "STP",
    *     "transfer_timestamp": 1645516741
      }
      }'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
