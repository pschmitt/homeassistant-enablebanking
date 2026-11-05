# Bank setup

Register an application in the [Enable Banking Control Panel](https://enablebanking.com/)
under **API applications**. Set its redirect URL to
`https://enablebanking.com/`, download its `.pem` private key, and copy the
application ID. Home Assistant 2026.4 or later is required. The same
application credentials can be reused for several bank entries. Home
Assistant stores the key in its config entry: protect your backups.

Add **Enable Banking** under **Settings → Devices & services → Add integration**.
Enter the entire key and application ID, select the bank's country, then
select the bank and Personal or Business account type. For Revolut Business,
select **Revolut** with **Business**, not a separate bank listing. The flow
shows a bank authorization link; sign in at the bank and copy only the
`code` query parameter from the final Enable Banking URL back into the flow.
If the link expires or fails, submit the empty code field for a fresh link.
The integration exchanges the code for a bank session and discovers accounts.
Repeat the flow for each additional bank.

The integration signs its own RS256 JWT with the application key and renews it
before expiry; there is no need to create a JWT manually. The repository's
`scripts/generate_jwt.py` is only a debugging tool, not an installation step.
See [Enable Banking's API quick start](https://enablebanking.com/docs/api/quick-start/)
for the provider's application setup.

If credentials are rejected, check that the key includes its PEM start and
end markers and that the application ID belongs to that key. If a bank link
returns `invalid_request`, request another link rather than reusing the old
one. A bank entry without account sensors may have been granted no accounts;
check the provider's application permissions and the Home Assistant logs.
