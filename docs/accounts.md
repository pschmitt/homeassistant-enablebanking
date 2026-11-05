# Account entities

Each discovered account has a monetary balance sensor with currency and
`state_class: total`. A closing booked balance is preferred over an interim
available balance. Sensor attributes include `iban`, `account_name`,
`product`, `currency`, `balance_type`, `reference_date`, `aspsp` (bank name),
`last_polled_at`, `last_error`, `stale`, `consent_expires_at` and
`consent_days_remaining`. The `transactions` attribute holds up to 50 recent
transactions from the previous 90 days, newest first, with amounts, currency,
dates and counterparty information supplied by the bank. These transactions
are not stored in Home Assistant's recorder.

One `event.<bank>_last_transaction` entity per bank fires a `transaction`
event for each newly observed transaction, oldest first. Its attributes
include the transaction fields and account identifiers. The first update
after a restart establishes a baseline rather than replaying cached items.
To notify on new transactions, replace this example event entity ID with the
one Home Assistant created:

```yaml
triggers:
  - trigger: state
    entity_id: event.example_bank_last_transaction
actions:
  - action: notify.notify
    data:
      message: >-
        {{ trigger.to_state.attributes.amount }}
        {{ trigger.to_state.attributes.currency }}
```

Add account sensors as ordinary tile cards on a Lovelace dashboard. Check
`last_error` and `stale` before treating an old displayed balance as current;
a bank or network failure does not erase the last saved balance.
