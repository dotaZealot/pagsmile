# Payin Status

## List of Payin status

| Status               | Description                                                                                       |
| -------------------- | ------------------------------------------------------------------------------------------------- |
| INITIAL              | The merchant created the order and waiting for the user to submit user info                       |
| EXPIRED              | Trade is expired                                                                                  |
| PROCESSING           | The user info has been submitted and waiting for the confirmation of payment                      |
| CANCEL               | Trade is canceled                                                                                 |
| REFUSED              | Trade has been refused                                                                            |
| SUCCESS              | Trade is successful                                                                               |
| REFUND\_VERIFYING    | The merchant submitted the refund and waiting for the user to provide bank info                   |
| REFUND\_PROCESSING   | Refund is processing                                                                              |
| REFUND\_REVOKE       | Refund is cancelled or expired                                                                    |
| REFUND\_REFUSED      | Refund is refused. Usually due to incorrect bank info                                             |
| REFUNDED             | Trade is refunded. Same for partial refund.                                                       |
| RISK\_CONTROLLING    | Trade is considered high risk or there is unclear billing information. Only appear for CreditCard |
| DISPUTE              | Trade is in dispute.  Only appear for CreditCard                                                  |
| CHARGEBACK           | Chargeback. Only appear for CreditCard                                                            |
| CHARGEBACK\_REVERSED | ChargebackReversed. Only appear for CreditCard                                                    |

## Payin status change flow

<figure><img src="../../.gitbook/assets/Pagsmile 2.0 Comm Flow.png" alt=""><figcaption></figcaption></figure>
