---
description: >-
  By integrating our JS library, it is a safer and more convenient way to use
  our services
---

# Pagsmile JavaScript

### Add the pagsmile.js file to your website <a href="#add-the-pagsmile-js-file-to-your-website" id="add-the-pagsmile-js-file-to-your-website"></a>

{% hint style="info" %}
It is not recommended to cache this js locally
{% endhint %}

```
<script src="https://res.pagsmile.com/lib/js/pagsmile.js"></script>
<script>
  Pagsmile.setPublishableKey('${app_id}','${public_key}','sandbox | prod')
</script>
```

### Create Pagsmile-specific form components <a href="#create-pagsmile-specific-form-components" id="create-pagsmile-specific-form-components"></a>

Ensure that the following fields exist in the existing form, and add the data-checkout attribute according to the format.

| Parameter                   | Required | Description                 |
| --------------------------- | -------- | --------------------------- |
| pagsmileCardNumber          | yes      | card number                 |
| pagsmileSecurityCode        | yes      | security code               |
| pagsmileCardExpirationYear  | yes      | expiration year (4 digits)  |
| pagsmileCardExpirationMonth | yes      | expiration month (2 digits) |
| pagsmileCardholderName      | yes      | holder name                 |
| pagsmileDocType             | no       | holder id type              |
| pagsmileDocNumber           | no       | holder id number            |

```
<ul>
    <li>
        <label for="cardNumber">Credit card number:</label>
        <input type="text" data-checkout="pagsmileCardNumber" />
    </li>
    <li>
        <label for="securityCode">Security code:</label>
        <input type="text" data-checkout="pagsmileSecurityCode" />
    </li>
    <li>
        <label for="cardExpirationYear">Expiration year:</label>
        <input type="text" data-checkout="pagsmileCardExpirationYear" />
    </li>
    <li>
        <label for="cardExpirationMonth">Expiration month:</label>
        <input type="text" data-checkout="pagsmileCardExpirationMonth" />
    </li>
    <li>
        <label for="cardholderName">Card holder name:</label>
        <input type="text" data-checkout="pagsmileCardholderName" />
    </li>
    <li>
        <label for="docType">Document type:</label>
        <select data-checkout="pagsmileDocType">
        </select>
    </li>
    <li>
        <label for="docNumber">Document number:</label>
        <input type="text" data-checkout="pagsmileDocNumber" />
    </li>
  </ul>
```

And add the following two components to the original form.

```
  <!-- token -->
  <input name="token" id="pagsmileToken" type="hidden">
  <!-- fingerprint -->
  <input name="fingerprint" id="pagsmileFingerprint" type="hidden">
```

### Monitor form submission events <a href="#monitor-form-submission-events" id="monitor-form-submission-events"></a>

Call before the original website submission event: Pagsmile.createToken function, pass in the form element and update the above two hidden fields.

```
  var $form = document.querySelector('#pay')
  Pagsmile.createToken($form, responseHandler)
```

### Bring the above two parameters and [place an order](../submit-a-payin/brazil/creditcard.md) <a href="#bring-the-above-two-parameters-and-place-an-order-through-api-direct-payment-api-direct" id="bring-the-above-two-parameters-and-place-an-order-through-api-direct-payment-api-direct"></a>

> The example code can be obtained from [here](https://res.pagsmile.com/lib/js/pagsmile\_template.html) (right click -> save as)
