# WalletKit configuration

This section describes the configuration files the _WalletKit_ instance needs to be set up with.

## Wallet configuration

Wallet configuration is specified by providing the `wallet-config.json` to the _WalletKit_ deployment.
It specifies the wallet urls (wallet app and wallet api), as well as the available issuers.

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

## Verifier configuration

Verifier configuration is specified by providing the `verifier-config.json` to the _WalletKit_ deployment.
It specifies the verifier urls (verifier app and verifier api), as well as the available wallets.
Set up the `allowedWebhookHosts` to the appropriate urls, if a custom callback is required to be executed
at the verification result.

Example configuration:

```json
{
  "verifierUiUrl": "https://verifier.walt-test.cloud",
  "verifierApiUrl": "https://verifier.walt-test.cloud/verifier-api/default",
  "wallets": {
    "walt.id": {
      "id": "walt.id",
      "url": "https://wallet.walt-test.cloud",
      "presentPath": "api/siop/initiatePresentation/",
      "receivePath": "api/siop/initiateIssuance/",
      "description": "walt.id web wallet"
    }
  },
  "allowedWebhookHosts": [
    "https://integrations.walt-test.cloud/callback/"
  ]
}
```

## Issuer configuration

Issuer configuration is specified by providing the `issuer-config.json` to the _WalletKit_ deployment.
It specifies the issuer urls (issuer app and issuer api), as well as the available wallet.

Example configuration:

```json
{
  "issuerUiUrl": "https://issuer.walt-test.cloud",
  "issuerApiUrl": "https://issuer.walt-test.cloud/issuer-api/default",
  "issuerClientName": "walt.id Issuer Portal",
  "wallets": {
    "walt.id": {
      "id": "walt.id",
      "url": "https://wallet.walt-test.cloud",
      "presentPath": "api/siop/initiatePresentation/",
      "receivePath": "api/siop/initiateIssuance/",
      "description": "walt.id web wallet"
    }
  }
}
```