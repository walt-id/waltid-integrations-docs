# Verifier configuration

verifier-config.json

Example configuration:

```json
{
  "verifierUiUrl": "https://verifier.cheqd.walt-test.cloud",
  "verifierApiUrl": "https://verifier.cheqd.walt-test.cloud/verifier-api/default",
  "wallets": {
    "walt.id": {
      "id": "walt.id",
      "url": "https://wallet.cheqd.walt-test.cloud",
      "presentPath": "api/siop/initiatePresentation/",
      "receivePath": "api/siop/initiateIssuance/",
      "description": "walt.id web wallet"
    }
  },
  "allowedWebhookHosts": [
    "https://integrations.cheqd.walt-test.cloud/callback/"
  ]
}
```