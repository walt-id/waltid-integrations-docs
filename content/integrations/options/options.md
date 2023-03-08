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

Wallet configuration specifies the wallet types available for issuance:

1. QR - mobile wallets:
    - Cross device flow: User uses another device (desktop pc, laptop) than where their wallet is installed (smartphone)
      .
    - In this case, you will use the virtual wallet "x-device", which creates an "openid-initiate-issuance://..." URL.
2. WEB - web wallets:
    - Same device flow: User uses the same device that their wallet is installed on.
    - In this case, you will have to additionally ask what web wallet the user is using (if you aren't forcing them to
      use your or a specific web wallet).
    - e.g. "walt.id", which creates an "https://wallet.walt.id/..." URL.
3. APP - app wallets
    - Theoretically same device flow, but also uses the virtual wallet "x-device" for creating an "
      openid-initiate-issuance://..." URL.

In the default configuration you can use the wallet "walt.id" (https://wallet.walt.id), or the virtual wallet "x-device"
for the cross device flow ("openid-initiate-issuance://...").

Setting `skipWalletChooserOnLastRemainingChoice` to `true` will replace the wallet multiple selection
element with a single selectable element when there's a single wallet type available.

## Messages

Options messages are key-value pairs mapped to a specific entity (e.g. issuer or verifier).
The keys follow the dot notation style. The following properties are available for wallet types (_qr_, _web_ and _app_):

- label
- provider
    - selection