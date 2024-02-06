---
description: >-
  IPN (Instant Payment Notification) is a notification sent from one server to
  another through an HTTP POST request informing your transactions.
---

# Notification

To receive notifications about the events in your platform, you have to previously configure the notification when you do the POST of the payment, indicating the URL in the field notify\_url.

{% swagger method="post" path="" baseUrl="$notify_url  which defined when submitting the payin transaction." summary="Notification" %}
{% swagger-description %}
Notification Parameters
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Pagsmile-Signature" required="true" %}
t=_$timestamp,v2=HMAC SHA256($_RequestBody_)_
{% endswagger-parameter %}

{% swagger-parameter in="body" name="trade_no" required="true" %}
Pagsmile transaction id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="out_trade_no" required="true" %}
merchant out\__trade\__no
{% endswagger-parameter %}

{% swagger-parameter in="body" name="out_request_no" required="false" %}
Pagsmile refund transaction id. Only for refund order
{% endswagger-parameter %}

{% swagger-parameter in="body" name="app_id" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="trade_status" required="true" %}
trade status.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="channel" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Merchant process the callback, and response "success"" %}
```javascript
success
```
{% endswagger-response %}
{% endswagger %}

### Events <a href="#events" id="events"></a>

Whenever an event occurs, we will send you a notification in json format using HTTP POST to the URL that you specified.

We will notify the following events:

| Action               | Description               |
| -------------------- | ------------------------- |
| SUCCESS              | Trade has been successful |
| CANCEL               | Trade has been cancelled  |
| EXPIRED              | Trade is expired          |
| REFUSED              | Trade has been refused    |
| CHARGEBACK           | Chargeback occurred       |
| CHARGEBACK\_REVERSED | Chargeback reversed       |
| REFUND\_REVOKE       | Refund revoke             |
| REFUND\_REFUSED      | Refund is refused         |
| REFUNDED             | Trade has been refunded   |
| DISPUTE              | Dispute occurred          |

We can notify the following events, contact us to set up if needed:

| Action             | Description                                                           |
| ------------------ | --------------------------------------------------------------------- |
| PROCESSING         | User has submitted the payment information                            |
| RISK\_CONTROLLING  | Trade is considered high risk or there is unclear billing information |
| REFUND\_VERIFYING  | Waiting for the user to submit refund information                     |
| REFUND\_PROCESSING | Refund information is received. Waiting for processing the refund.    |

Pagsmile will send notifications with the following schedule of retries and confirmation waiting times. You must return an HTTP STATUS 200 (OK) with response data "success" before the corresponding time expires. If not, it will be assumed that you did not receive it correctly and you will be notified again.

It is recommended that you respond to the notification before executing business logic or before accessing external resources so as not to exceed the estimated response times.

This communication is exclusively between the servers of Pagsmile and your server, so there will not be a physical user seeing any type of result.

| Event     | Time after the first dispatch |
| --------- | ----------------------------- |
| Dispatch  | -                             |
| 1st retry | 10 minutes                    |
| 2nd retry | 30 minutes                    |
| 3rd retry | 60 minutes                    |
| 4th retry | 120 minutes                   |
| 5th retry | 360 minutes                   |
| 6th retry | 840 minutes                   |

## Verifying signatures (optional) <a href="#verifying-signatures-manually" id="verifying-signatures-manually"></a>

The approximate content of the Pagsmile-Signature header is as follows (here with line breaks for easy viewing, the actual content is all on one line):

```
Pagsmile-Signature:
t=1577808000,
v2=5257a869e7ecebeda32affa62cdca3fa51cad7e77a0e56ff536d0ce8e108d8bd
```

The Pagsmile-Signature header contains a timestamp and a signature. The timestamp is prefixed by t=, followed by a UNIX timestamp; the signature is prefixed by v2=, followed by the signature content.

#### Step 1 : Extract the timestamp and signatures from the header <a href="#step-1-extract-the-timestamp-and-signatures-from-the-header" id="step-1-extract-the-timestamp-and-signatures-from-the-header"></a>

Split the header using the \[,] character as the separator, to get a list of elements. Then split each element using the \[=] character as the separator, to get a prefix and value pair.

The value for the prefix \[t] corresponds to the timestamp, and \[v2] corresponds to the signature. You can discard all other elements.

#### Step 2 : Prepare the **original** RequestBody string <a href="#step-2-prepare-the-original-requestbody-string" id="step-2-prepare-the-original-requestbody-string"></a>

Get all the content in the RequestBody. Please pay attention here. <mark style="background-color:red;">**Please do not use the program's self-built structure to format and/or serialize the RequestBody content**</mark>. If you have similar requirements, please do it after getting the original data for verification to avoid unnecessary sorting of fields and the addition of characters affecting the signature.

#### Step 3 : Determine the expected signature <a href="#step-3-determine-the-expected-signature" id="step-3-determine-the-expected-signature"></a>

Compute an HMAC with the SHA256 hash function. Use the SecretKey get from The merchant dashboard as the key(salt), and use the original RequestBody string as the message.

#### Step 4 : Compare the signatures <a href="#step-4-compare-the-signatures" id="step-4-compare-the-signatures"></a>

Compare the signature in the header to the expected signature. For an equality match, compute the difference between the current timestamp and the received timestamp, then decide if the difference is within your tolerance.

### Notification Example

{% hint style="warning" %}
The following notification is only an example. Different methods can have more or less parameters in the real notification. Please refer to what you received when testing.
{% endhint %}

```
Content-Type: application/json
Method: POST
Header: t=1645516741, v2=f6e345eca80d74c470ba456b7b559046f22b49fcaad9b81938ff1488b0f497ac
Body:
  {
    "amount": "12.01",
    "out_trade_no": "202201010354002",
    "method": "Boleto",
    "channel": "",
    "trade_status": "SUCCESS",
    "trade_no": "2022022201111100011",
    "currency": "BRL",
    "out_request_no": "",
    "app_id": "162************38",
    "timestamp": "1645516741",
    "user":{
      "buyer_id": "",
      "identify":{
        "type": "CPF",
        "number": "50284414727"
      },
      "username": "test user name",
      "phone": "75991435892",
      "email": "test@pagsmile.com",
      "ip": ""
    }
  }
```

{% hint style="danger" %}
Please contact us to get the IP addresses that our notifications will be sent from.
{% endhint %}
