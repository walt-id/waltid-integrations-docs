# Wallet configuration

wallet-config.json

Example configuration:

```json
{
  "walletUiUrl": "https://wallet.walt-test.cloud",
  "walletApiUrl": "https://wallet.walt-test.cloud/api",
  "issuers": {
    "walt.id": {
      "id": "walt.id",
      "url": "https://issuer.walt-test.cloud/issuer-api/oidc",
      "description": "walt.id Issuer Portal"
    },
    "yes.com": {
      "id": "yes.com",
      "url": "https://demo.sandbox.yes.com/essif/issuer/c2id",
      "description": "yes.com Bank ID issuer"
    },
    "onboarding@walt.id": {
      "id": "onboarding@walt.id",
      "url": "https://issuer.walt-test.cloud/onboarding-api/oidc",
      "description": "walt.id On-Boarding service"
    }
  }
}
```