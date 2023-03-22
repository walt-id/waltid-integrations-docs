# Configure Issuer

Setting up the Issuer through the issuer config. If you haven't created your did yet, please refer back to [Create a DID](create-a-did/) and create one.

{% hint style="info" %}
As the wallet-kit supports [multi-tenancy](../../../deep-dive/multi-tenancy.md), It is important to decide if you want to use the default tenant with the id `default` or [create a new one](https://app.gitbook.com/s/rhL2aTXU1w6MO3blK9B1/getting-started/rest-apis/issuer-configuration#multi-tenancy). In the examples, we will be using the default one.
{% endhint %}

## Get default Issuer Config

Use the default tenant to get the config. When updating, use the tenant you are working with.

{% tabs %}
{% tab title="REST API" %}
You can optionally use the [Swagger doc](http://localhost:8080/api/swagger#/Issuer%20Configuration/getConfiguration) to make the request.\
\
**Request in with CURL**&#x20;

```bash
curl -X 'GET' \
  'http://localhost:8080/issuer-api/{tenantId}/config/getConfiguration'
```



**Path parameters**

* `tenantId`: _**\[string]**_ tenant from which to get the config.\


**Example**

```bash
curl -X 'GET' \
  'http://localhost:8080/issuer-api/default/config/getConfiguration'
```
{% endtab %}
{% endtabs %}

## Update Issuer Config

{% tabs %}
{% tab title="REST API" %}
You can optionally use the [Swagger doc](http://localhost:8080/api/swagger#/Issuer%20Configuration/setConfiguration) to make the request.\
\
**Request in with CURL**&#x20;

```bash
curl -X 'POST' \
  'http://localhost:8080/issuer-api/{{tenantId}}/config/did/createAdvanced' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "issuerApiUrl": "string",
  "issuerClientName": "string",
  "issuerDid": "string",
  "issuerUiUrl": "string",
  "wallets": {
    "waltid": {
      "description": "string",
      "id": "string",
      "presentPath": "string",
      "receivePath": "string",
      "url": "string"
    }
  }
}'
```

**Path parameters**

* `tenantId`: _**\[string]**_ tenant from which to update the config.



**Body paramters**

```
{
  "issuerApiUrl": "string",
  "issuerClientName": "string",
  "issuerDid": "string",
  "issuerUiUrl": "string",
  "wallets": {
    "{walletKey}": {
      "description": "string",
      "id": "string",
      "presentPath": "string",
      "receivePath": "string",
      "url": "string"
    }
  }
}
```

* `issuerApiUrl`: _**\[string]**_ the url of the the wallet-kit issuer-api + your tenant. Example: http://localhost:8080/issuer-api/default&#x20;
* `issuerClientName`: _**\[string]**_ name for the client. Example: Walt.id Issuer Portal
* `issuerDid`: _**\[string]**_ the did created in the [Create a Did](create-a-did/) section
*   `wallets`: _**\[object]**_ List of wallets for credential issuance. Each wallet is defined with it's name as key an an object (the config of the wallet) as a value.

    **Config Object**

    * `description`: _**\[string]**_ description of the wallet: Example: walt.id web wallet
    * `id`: _**\[string]**_ identifier for the wallet in the wallet-kit. Example: waltid
    * `presentPath`: _**\[string]**_ path that handles the initialisation of a VC presentation. Example: api/siop/initiatePresentation/
    * `receivePath`: _**\[string]**_ path handling the receiving of a VC. Example: api/siop/initiateIssuance/
    * `url`: _**\[string]**_ the url where the wallet is hosted. Example: localhost:3000, if you are using the local version of the [web-wallet](../web-wallet.md) and which we setup later.

\


**Example**

```bash
curl -X 'POST' \
  'http://localhost:8080/issuer-api/default/config/setConfiguration' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "issuerApiUrl": "http://localhost:8080/issuer-api/default",
  "issuerClientName": "Walt.id Issuer Portal",
  "issuerDid": "did:key:z6MknN2cB2gbNyTiRvX4FdH27Mttc5My9EyfkT4yXhGHx9D2",
  "issuerUiUrl": "http://localhost:8000",
  "wallets": {
    "waltid": {
      "description": "walt.id web wallet",
      "id": "waltid",
      "presentPath": "api/siop/initiatePresentation/",
      "receivePath": "api/siop/initiateIssuance/",
      "url": "http://localhost:3000"
    }
  }
}'
```
{% endtab %}
{% endtabs %}
