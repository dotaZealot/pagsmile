---
description: This integration requires PCI Certification.
---

# PCI Direct Integration

## Create an Order

{% tabs %}
{% tab title="Create Card Payment" %}
Here are the steps to create a card payment.

Step 1, Get Token. Check [Tokenization](tokenize.md) page.

Step 2, Create a Credit Card order. Check [this](creditcard.md) page.
{% endtab %}

{% tab title="Authorize Card Payment" %}
Here are the steps to authorize a card payment.

Step 1, Get Token. Check [Tokenization](tokenize.md) page.

Step 2, Authorization. Check [Authorization](authorization.md) page.

Step 3, Capture. Check [Capture](caputre.md) page.

Step 4, Void if no longer needed. Check [Void](void.md) page.
{% endtab %}
{% endtabs %}

## Refund

Use [refund API](../refund.md) to refund an order.

## Query

Use [query API](../payin-detail.md) to check order details.

## Notification

Receive [notification](../notification/) for order status update.
