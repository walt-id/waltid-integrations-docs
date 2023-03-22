# Custom Templates

A custom template is **a user-defined structure for Verifiable Credentials** that addresses specific use cases or requirements **not covered by the default templates provided by Wallet-Kit**. By defining unique credential templates, you can **incorporate additional attributes specific to your project needs**.

{% hint style="info" %}
As the wallet-kit supports [multi-tenancy](../../../../deep-dive/multi-tenancy.md), It is important to decide if you want to use the default tenant with the id `default` or [create a new one](https://app.gitbook.com/s/rhL2aTXU1w6MO3blK9B1/getting-started/rest-apis/issuer-configuration#multi-tenancy). In the examples, we will be using the default one.
{% endhint %}

### Defining MyCustomCredential

1.  **Define the `@context` field**, which should include the standard Verifiable Credential context and any additional contexts relevant to your application:

    ```scss
    "@context": [
      "https://www.w3.org/2018/credentials/v1",
      "https://www.w3.org/2018/credentials/examples/v1",
      "https://example.com/custom-context/v1"
    ],
    ```


2.  **Specify the `type` field**, which should include the standard Verifiable Credential type and your custom credential type:

    ```json
    "type": [
      "VerifiableCredential",
      "MyCustomCredential"
    ],
    ```


3.  Add the `id` field, which uniquely identifies your custom credential:

    ```json
    "id": "http://example.com/credentials/12345",
    ```


4.  Define the `issuer` field, which specifies the decentralized identifier (DID) of the issuer. This field will be populated with the issuer setup in the [Configure Issuer](../configure-issuer.md) section:

    ```json
    "issuer": {
      "id": "did:example:issuer"
    },
    ```


5.  Add the `credentialSubject` field, which contains the custom data fields, properties, or attributes that you want to include in your credential:

    ```json
    "credentialSubject": {
      "id": "did:example:subject",
      "customField1": "Some data",
      "customField2": {
        "subField1": "More data",
        "subField2": 123
      }
    }
    ```

Here's the complete custom credential:

```json
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1",
    "https://example.com/custom-context/v1"
  ],
  "type": [
    "VerifiableCredential",
    "MyCustomCredential"
  ],
  "id": "http://example.com/credentials/12345",
  "issuer": {
    "id": "did:example:issuer"
  },
  "credentialSubject": {
    "id": "did:example:subject",
    "customField1": "Some data",
    "customField2": {
      "subField1": "More data",
      "subField2": 123
    }
  }
}
```

This custom credential can now be used to create a template based on it via the Wallet-Kit API. \


### Creating the template

{% tabs %}
{% tab title="REST API" %}
You can optionally use the [Swagger doc](http://localhost:8080/api/swagger#/Issuer%20Configuration/importTemplate) to make the request.\
\
**Request in with CURL**&#x20;

```bash
curl -X 'POST' \
  'http://localhost:8080/issuer-api/{tenantId}/config/templates/{templateId}' \
  -H 'accept: text/plain' \
  -H 'Content-Type: application/json' \
  -d '{MyCustomCredential}'
```



**Path parameters**

* `tenantId`: _**\[string]**_ tenant from which to get the templates from.
* `templateId`: _**\[string]**_ the id for the template. Example: MyCustomCredential



**Body**

Please refer to [Defining MyCustomCredential](custom-templates.md#defining-mycustomcredential). Use the final JSON of the credential as body.\


**Example**

```bash
curl -X 'POST' \
  'http://localhost:8080/issuer-api/default/config/templates/MyCustomCredential' \
  -H 'accept: text/plain' \
  -H 'Content-Type: application/json' \
  -d '{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1",
    "https://example.com/custom-context/v1"
  ],
  "type": [
    "VerifiableCredential",
    "MyCustomCredential"
  ],
  "id": "http://example.com/credentials/12345",
  "issuer": {
    "id": "did:example:issuer"
  },
  "credentialSubject": {
    "id": "did:example:subject",
    "customField1": "Some data",
    "customField2": {
      "subField1": "More data",
      "subField2": 123
    }
  }
}'
```
{% endtab %}
{% endtabs %}



### Deleting the template

{% tabs %}
{% tab title="First Tab" %}
You can optionally use the [Swagger doc](http://localhost:8080/api/swagger#/Issuer%20Configuration/importTemplate) to make the request.\
\
**Request in with CURL**&#x20;

```bash
curl -X 'DELETE' \
  'http://localhost:8080/issuer-api/{tenantId}/config/templates/{templateId}' \
  -H 'accept: text/plain'
```



**Path parameters**

* `tenantId`: _**\[string]**_ tenant from which to delete the template.
* `templateId`: _**\[string]**_ the id for the template. Example: MyCustomCredential\


**Example**

```bash
curl -X 'DELETE' \
  'http://localhost:8080/issuer-api/default/config/templates/MyCustomCredential' \
  -H 'accept: text/plain'
```
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}
