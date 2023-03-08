# Setup issuer configuration

By default, any newly created tenant is configured with an empty DID value.
It is required to update the configuration so it is set up with the DID created
in the [create-tenant-did](create-tenant-did.md) section.

## Retrieve the current issuer configuration

GET /issuer-api/{tenantId}/config/getConfiguration

```shell
curl -X 'GET' \
  'https://wallet.walt-test.cloud/issuer-api/default/config/getConfiguration' \
  -H 'accept: application/json'
```

Response:

```json
{
  "issuerUiUrl": "https://issuer.walt-test.cloud",
  "issuerApiUrl": "https://issuer.walt-test.cloud/issuer-api/default",
  "issuerClientName": "walt.id Issuer Portal",
  "wallets": {
    "walt.id": {
      "id": "walt.id",
      "url": "https://wallet.walt-test.cloud",
      "description": "walt.id web wallet",
      "presentPath": "api/siop/initiatePresentation/",
      "receivePath": "api/siop/initiateIssuance/"
    }
  }
}
```

## Update issuer configuration

POST /issuer-api/{tenantId}/config/setConfiguration

```shell
curl -X 'POST' \
  'https://wallet.walt-test.cloud/issuer-api/default/config/setConfiguration' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d 'vv JSON BELOW vv'
```

```json
{
  "issuerUiUrl": "https://issuer.walt-test.cloud",
  "issuerApiUrl": "https://issuer.walt-test.cloud/issuer-api/default",
  "issuerClientName": "walt.id Issuer Portal",
  "issuerDid": "did:key:z6MknaJ7YLdkCq1QV2tcwVSY5uVfUKGfBdigo7g4PyipTnCc",
  "wallets": {
    "walt.id": {
      "id": "walt.id",
      "url": "https://wallet.walt-test.cloud",
      "description": "walt.id web wallet",
      "presentPath": "api/siop/initiatePresentation/",
      "receivePath": "api/siop/initiateIssuance/"
    }
  }
}
```

The configuration was amended to include the "issuerDid"
attribute with the DID from "Creating a DID for a tenant".