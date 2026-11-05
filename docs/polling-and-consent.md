# Polling and consent

PSD2 limits unattended account-information access to four polls per day per
consent. The integration schedules polls at 10:00, 14:00, 18:00 and 22:00
local time, with a deterministic minute offset per bank entry. It keeps the
last successful balance on disk in Home Assistant storage so a restart does
not needlessly spend quota. If Home Assistant was offline through a scheduled
slot, one catch-up poll starts with jitter. A rate-limited account backs off
for its next scheduled slot; other accounts can continue. Network, API,
consent and rate-limit failures preserve the last known value. `last_error`
shows a failure category and `stale` becomes true after 16 hours without a
successful poll. `enablebanking.refresh` polls configured entries on demand;
use it sparingly because it spends quota.

Bank consent has a finite term (up to 180 days). The integration warns in
Home Assistant 14 days before expiry. Use the bank entry's **Reconfigure**
action under **Settings → Devices & services → Enable Banking** to authorize
again before it expires. If a session has expired or the bank revokes it, the
entry requests reauthentication; a still-valid session can be revalidated
without another bank login. The cached balance remains visible but is not a
fresh reading. The application key is reused for renewal; do not generate a
new key unless the old one was revoked at Enable Banking.
