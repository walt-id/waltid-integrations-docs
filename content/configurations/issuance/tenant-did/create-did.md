# Creating a DID for a tenant

POST /issuer-api/{tenantId}/config/createDid

POST this JSON body to the specified URL:

```json
{
  "method": "string*",
  "keyAlias": "string",
  "didWebDomain": "string",
  "didWebPath": "string"
}
```

Method being one of: [ key, web, ebsi, iota, cheqd, jwk ].  
Only the method is required. All "didWeb" prefixed options are only needed for creating a did:web.

#### Example:

```shell
curl -X 'POST' \
  'https://wallet.walt-test.cloud/issuer-api/default/config/createDid' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "method": "key",
}'
```

Response: `did:key:z6MknaJ7YLdkCq1QV2tcwVSY5uVfUKGfBdigo7g4PyipTnCc`