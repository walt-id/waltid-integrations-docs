# Options integrations

The _options_ feature allows having customizable properties configured for the enabled platform integrations
(such as wallet selection messages and configurations).

E.g. discord integration options
```json
{
  "messages": {
    "discord.walletselector.verifier": {
      "web.label": "Web wallet",
      "web.provider.selection": "Select web wallet provider",
      "action.link": "Share with %s",
      "wallet.select": ""
    },
    "discord.walletselector.issuer": {
      "web.label": "Web wallet",
      "web.provider.selection": "Select web wallet provider",
      "action.link": "Claim your cred on %s",
      "wallet.select": ""
    }
  },
  "walletConfiguration": {
    "activeWalletTypes": [
      {
        "id": "qr",
        "type": "QR"
      },
      {
        "id": "web",
        "type": "WEB"
      },
      {
        "id": "app",
        "type": "APP"
      }
    ],
    "skipWalletChooserOnLastRemainingChoice": true
  }
}
```

## Wallet configuration

Wallet configuration specifies the wallet types available for issuance / verification:

- QR - mobile wallet
- WEB - web wallet
- APP - desktop wallet

Setting `skipWalletChooserOnLastRemainingChoice` to `true` will replace the wallet multiple selection
element with a single selectable element when there's a single wallet type available.

## Messages

Options messages are key-value pairs mapped to a specific entity (e.g. issuer or verifier).
The keys follow the dot notation style. The following properties are available for wallet types (_qr_, _web_ and _app_):

- label
- provider
    - selection