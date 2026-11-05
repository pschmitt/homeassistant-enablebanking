<p align="center">
  <a href="https://my.home-assistant.io/redirect/marketplace_repository/?owner=pschmitt&amp;repository=homeassistant-enablebanking&amp;category=integration"><img src="https://my.home-assistant.io/badges/marketplace_repository.svg" alt="Open this integration in Home Assistant Marketplace"></a>
</p>

<h1 align="center">Enable Banking for Home Assistant</h1>

<p align="center">Show account balances and recent transactions from banks supported by Enable Banking.</p>

Home Assistant 2026.4 or later and an [Enable Banking](https://enablebanking.com/)
application are required. Each bank has its own config entry.

## Features

- **Bank balances:** Create a monetary sensor per account, with currency, bank and recent transaction attributes. See [Account entities](docs/accounts.md).
- **Transaction events:** Emit newly observed transactions without replaying the previous poll after a restart.
- **Quota-aware polling:** Run four scheduled polls per day per entry and retain balances when a bank is unavailable. See [Polling and consent](docs/polling-and-consent.md).
- **Consent renewal:** Warn before bank authorization expires and reauthorize through Home Assistant's integration UI.
- **Signed API tokens:** Create and renew the Enable Banking JWT from the application's stored private key. See [Bank setup](docs/bank-setup.md).

## Install

Use the Marketplace badge above on Home Assistant 2026.11 or later to add this
repository as a custom integration. On older versions, add it as a HACS
custom repository of type **Integration**. Install and restart Home Assistant.
The badge does not imply a public catalog listing. For manual installation,
copy `custom_components/enablebanking/` into Home Assistant's
`custom_components/` directory and restart.

## Quick start

1. Register an Enable Banking API application and download its private key. See [Bank setup](docs/bank-setup.md).
2. Add **Enable Banking** under **Settings → Devices & services → Add integration**.
3. Enter the application ID and key, select a country and bank, and complete bank authorization.
4. Add the resulting balance sensor to a dashboard.

## Documentation

| Topic | Description |
|-------|-------------|
| [Bank setup](docs/bank-setup.md) | API application, authorization and troubleshooting |
| [Account entities](docs/accounts.md) | Balances, transactions and dashboard examples |
| [Polling and consent](docs/polling-and-consent.md) | Poll limits, cached data and reauthorization |
| [Changelog](CHANGELOG.md) | Release history |

## License

[MIT](LICENSE).
