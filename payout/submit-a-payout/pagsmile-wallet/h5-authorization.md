---
description: H5 application get user authorization
---

# H5 Authorization

1. Provide the authorization link to users.

The authorization link is concatenated with Basic URL+notify\__url+reference\_id+source+sign\_key_

| Parameter     | Explaination                                            | Example value            |
| ------------- | ------------------------------------------------------- | ------------------------ |
| notify\_url   | the url that used to receive notification               | https://www.pagsmile.com |
| reference\_id | merchant user's id. Defined by merchant                 | 20220101123              |
| source        | a string which can recognize the merchant               | pagsmile                 |
| sign\_key     | a key used for verifying signature. Defined by merchant | test\_key                |

{% hint style="danger" %}
Don't put # sign in the URL
{% endhint %}

{% tabs %}
{% tab title="Test environment" %}
Basic URL

```
https://sandbox-wallet.pagsmile.com/authenticationH5?
```



Example:

```
https://sandbox-wallet.pagsmile.com/authenticationH5?notify_url=https://www.pagsmile.com&reference_id=1234567&source=abc&sign_key=test_key
```
{% endtab %}

{% tab title="Live environment" %}
Basic URL

```
https://wallet.pagsmile.com/authenticationH5?
```



Example:

```
https://wallet.pagsmile.com/authenticationH5?notify_url=https://www.pagsmile.com&reference_id=1234567&source=abc&sign_key=test_key
```
{% endtab %}
{% endtabs %}

Users will be redirected to this page to authorize.

![](<../../../.gitbook/assets/image (15).png>)



2\. Users authorize and the merchant gets UUID.

After users authorized on the page from Step 1. Users will be redirected to the notification page_. The page URL will be concatenated with notify\_url+merchant\_user\_id+pagsmile\_id+phone\_number+sign_

| Parameter            | Explaination                                                         | Example |
| -------------------- | -------------------------------------------------------------------- | ------- |
| merchant\__user\__id | the reference\_id is provided in step 1.                             |         |
| pagsmile\_id         | user's UUID                                                          |         |
| phone\_number        | phone number                                                         |         |
| sign                 | signature generated with sign_key. sign\_key is provided in step 1._ |         |

Signature rule:

```
let param = 'merchant_user_id=' + reference_id + '&pagsmile_id=' + uuid + '&phone_number' + phone_number;
let sign = param + '&key=' + sign_key;
sign = md5(md5(sign));
```

Example of the URL of notification page

```
https://www.pagsmile.com/?merchant_user_id=1234567&pagsmile_id=b5e8b5d94bbafdd7be8d91e784a7413d&phone_number=177****1868&sign=4b7841cf03c6011d2137b99a20f82d61
```



3\. Merchant needs to link merchant's user ID with the UUID of Pagsmile wallet. Then users can be redirected to the other page as needed.
