# Cross device flow

```
https://wallet.walt-test.cloud/verifier-api/{tenantId}/presentXDevice
```

Available parameters:

- tenantId: Tenant Id, by default "default"
- vcType: Array<String>, select your VC type IDs, e.g. "VerifiableId"
- schemaUri: Array<String>, can be used instead of vcType to specify by schema URI instead of VC type

```shell
curl -X 'GET' \
  'https://wallet.walt-test.cloud/verifier-api/default/presentXDevice?vcType=VerifiableId' \
  -H 'accept: application/json'
```

Example response:

```json
{
  "requestId": "82dcbb5a-e5b3-447d-bc25-b22d7cfa4445",
  "url": "openid://?scope=openid&presentation_definition=%7B%22format%22+%3A+null%2C+%22id%22+%3A+%221%22%2C+%22input_descriptors%22+%3A+%5B%7B%22constraints%22+%3A+%7B%22fields%22+%3A+%5B%7B%22filter%22+%3A+%7B%22const%22%3A+%22VerifiableId%22%7D%2C+%22id%22+%3A+null%2C+%22path%22+%3A+%5B%22%24.type%22%5D%2C+%22purpose%22+%3A+null%7D%5D%7D%2C+%22format%22+%3A+null%2C+%22group%22+%3A+null%2C+%22id%22+%3A+%221%22%2C+%22name%22+%3A+null%2C+%22purpose%22+%3A+null%2C+%22schema%22+%3A+null%7D%5D%2C+%22name%22+%3A+null%2C+%22purpose%22+%3A+null%2C+%22submission_requirements%22+%3A+null%7D&response_type=vp_token&redirect_uri=http%3A%2F%2Flocalhost%3A8080%2Fverifier-api%2Fdefault%2Fverify&state=82dcbb5a-e5b3-447d-bc25-b22d7cfa4445&nonce=82dcbb5a-e5b3-447d-bc25-b22d7cfa4445&client_id=http%3A%2F%2Flocalhost%3A8080%2Fverifier-api%2Fdefault%2Fverify&response_mode=post"
}
```