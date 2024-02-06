---
description: How to verify our notifications.
---

# Notification

Once the payout is confirmed by the bank, Pagsmile will send a notification to the merchant notification URL informing you of the result of the transaction. This URL is defined when submitting the payout transaction, by using the _notify\_url_ parameter for each payout request. Notification will retry 6 times when your processing failed.

{% swagger baseUrl="$notify_url" path=" which defined when submitting the payout transaction." method="post" summary="Notifcation" %}
{% swagger-description %}
Notification Parameters
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
SHA256(_$sorted\_params + $app_\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="payoutId" type="string" required="true" %}
pagsmile transaction id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" type="string" required="true" %}
merchant custom\_code
{% endswagger-parameter %}

{% swagger-parameter in="body" name="status" type="string" required="true" %}
PAID or REJECTED
{% endswagger-parameter %}

{% swagger-parameter in="body" name="msg" type="string" %}
success or rejected message
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" type="integer" required="true" %}
unix timestamp
{% endswagger-parameter %}

{% swagger-response status="200" description="Merchant process the callback, and response "success"" %}
```
success
```
{% endswagger-response %}
{% endswagger %}

## Authorization Check

* Get callback's body parameters, and sort them ascendingly.
* Concatenate _sorted\_params with app\_key._
* Use _sha256(sorted\_params + app\_key)_ to generate **App Authorization**.
* Get **Pagsmile Authorization** from callback's Header.
* Verify if **Pagsmile Authorization** matches with **App Authorization**.

{% hint style="danger" %}
When sorting parameters, strip the ones with no value.
{% endhint %}

## Notification Events

* PAID
* REJECTED
* REFUNDED

{% hint style="danger" %}
By now, both _**SPEI & Pagsmile Wallet**_ supported _**REFUNDED**_ notification_**.**_
{% endhint %}

## Notification Example

```
curl --location --request POST $your_notify_url \
--header 'Authorization: $pagsmile_authorization' \
--header 'Content-Type: application/json' \
--data-raw '{
    "payoutId": "TS202202071548044sGt3ADbmpGsPB",
    "custom_code": "custom_code_test",
    "status": "PAID",
    "msg": "success",
    "timestamp": 1628564650
}'
```

## Notification Retries

Pagsmile will send notifications with the following schedule of retries and confirmation awaiting times. You must return an HTTP STATUS 200 (OK) with response data "success" before the corresponding time expires. If not, it will be assumed that you did not receive it correctly and you will be notified again.

It is recommended that you respond to the notification before executing business logic or prior to accessing external resources so as not to exceed the estimated response times.

This communication is exclusively between the servers of Pagsmile and your server, so there will not be a physical user seeing any type of result.

| Event     | Time after first dispatch |
| --------- | ------------------------- |
| Dispatch  | --                        |
| 1st retry | 10 minutes                |
| 2nd retry | 30 minutes                |
| 3rd retry | 60 minutes                |
| 4th retry | 120 minutes               |
| 5th retry | 360 minutes               |
| 6th retry | 840 minutes               |

{% hint style="danger" %}
Our notifications will be sent from these IP addresses, please add them to your whitelist.
{% endhint %}
