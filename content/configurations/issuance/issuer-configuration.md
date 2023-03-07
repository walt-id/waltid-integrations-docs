# Issuer configuration

issuer-config.json

Example configuration:

```json
{
  "issuerUiUrl": "https://issuer.cheqd.walt-test.cloud",
  "issuerApiUrl": "https://issuer.cheqd.walt-test.cloud/issuer-api/default",
  "issuerClientName": "walt.id Issuer Portal",
  "wallets": {
    "walt.id": {
      "id": "walt.id",
      "url": "https://wallet.cheqd.walt-test.cloud",
      "presentPath": "api/siop/initiatePresentation/",
      "receivePath": "api/siop/initiateIssuance/",
      "description": "walt.id web wallet"
    }
  }
}
```