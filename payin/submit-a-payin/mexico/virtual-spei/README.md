---
description: How to use virtual SPEI to submit a payin in Mexico.
---

# Virtual SPEI

## Overviews

1.  You collect the following customer details:&#x20;

    A. Your customer's name\&email.&#x20;

    B. Your customer's user\_id on your platform.&#x20;

    C. Your customer's identity.&#x20;
2. You make a clabe transfer account create request with the customer's details. Check [API](create.md).
3. Persist the clabe account number and account id in your database, and informcustomer theclabe.&#x20;
4. This account has no expiration date, user can transfer money to this clabe account number anytime.&#x20;
5. Pagsmile will receive a notification from the bank, after the transfer is successful.
6. Then you will receive a notification from pagsmile with the account number

<figure><img src="../../../../.gitbook/assets/virtual account flow.png" alt=""><figcaption><p>Virtual SPEI Flow</p></figcaption></figure>
