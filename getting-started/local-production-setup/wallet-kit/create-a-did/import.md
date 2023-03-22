# Import

{% hint style="info" %}
As the wallet-kit supports [multi-tenancy](../../../../deep-dive/multi-tenancy.md), It is important to decide if you want to use the default tenant with the id `default` or [create a new one](https://app.gitbook.com/s/rhL2aTXU1w6MO3blK9B1/getting-started/rest-apis/issuer-configuration#multi-tenancy). In the examples, we will be using the default one.
{% endhint %}

### Import Key

{% tabs %}
{% tab title="REST API" %}
You can optionally use the [Swagger doc](http://localhost:8080/api/swagger#/Key%20Management/importKey) to make the request.\
\
**Request in with CURL** \
****We will import a key in JWK. PEM is also supported.

```bash
curl -X 'POST' \
  'http://localhost:8080/issuer-api/{tenantId}/config/key/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "kty": "string",
    "d": "string",
    "use": "string",
    "crv": "string",
    "kid": "string",
    "x": "string",
    "alg": "string"
}'
```

**Path parameters**

* `tenantId`: _**\[string]**_ tenant on which to create the did.

****\
**Body paramters**\
****Key in JWK

```
{
    "kty": "string",
    "d": "string",
    "use": "string",
    "crv": "string",
    "kid": "string",
    "x": "string",
    "alg": "string"
}
```

* &#x20;`kty` : (Key Type) A string that identifies the cryptographic algorithm family used with the key. Example:  "kty": "OKP" .
* `d` : (Private Key) A string that represents the private key. Example:  "d": "s3s3" . 
* `use` : (Public Key Use) A string that specifies how the key is intended to be used. Example:  "use": "sig" .
* `crv` : (Curve) A string that identifies the cryptographic curve used with the key. Example:  "crv": "Ed25519" .
* `kid` : (Key ID) A string that identifies the key. Example:  "kid": "my-key-id" . 
* `x` : (X Coordinate) A string that represents the x-coordinate of the public key. Example:  "x": "s3s3" . 
* `alg` : (Algorithm) A string that identifies the cryptographic algorithm used with the key. Example:  "alg": "EdDSA" .\


**Example**

```bash
curl -X 'POST' \
  'http://localhost:8080/issuer-api/default/config/key/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "kty": "OKP",
    "d": "9uq85sAD_RHrN_IC-rqk8UbTD0XbHSCCQ5A3Etfv6p0",
    "use": "sig",
    "crv": "Ed25519",
    "kid": "fc184a709db743f2ae67923f700aa7e6",
    "x": "gFMIlgEPLYN6_7JOu00LUtQ5YpW1bDBHz66KeYpA_z4",
    "alg": "EdDSA"
}'
```
{% endtab %}

{% tab title="CLI" %}
### Import Key

\
We will import a key in JWK. PEM is also supported, learn more in our [SSI-Kit ](#user-content-fn-1)[^1][Docs](https://docs.walt.id/v/ssikit/getting-started/cli-command-line-interface/key-management#import-key).

```
walletkit config --as-issuer default key import {{filePath}}
```

**Flags**

* `--as-issuer | -i`  - The config command let's you define the context in which you want to execute the command, by specifiying the arguments _--as-issuer_, _--as-verifier_ or _--as-user \[userID]_ or their shortcuts _-i_, _-v_, _-u \[userID]_

**Variables**

* `filePath` - path to JWK key file.\


#### **Example Command**

```
walletkit config -i default key import myKey.json
```

\
myKey.json

```json
{
  "kty": "OKP",
  "d": "9uq85sAD_RHrN_IC-rqk8UbTD0XbHSCCQ5A3Etfv6p0",
  "use": "sig",
  "crv": "Ed25519",
  "kid": "fc184a709db743f2ae67923f700aa7e6",
  "x": "gFMIlgEPLYN6_7JOu00LUtQ5YpW1bDBHz66KeYpA_z4",
  "alg": "EdDSA"
}
```
{% endtab %}
{% endtabs %}





### Import DID & DID document

{% tabs %}
{% tab title="REST API" %}
You can optionally use the [Swagger doc](http://localhost:8080/api/swagger#/Decentralized%20Identifiers/importDid) to make the request.\
\
**Request with CURL** \
****Will resolve and import the DID

```bash
curl -X 'POST' \
  'http://localhost:8080/issuer-api/{tenantId}/config/did/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "@context": "string",
    "id": "string",
    "controller": ["string"],
    "authentication": ["string"],
    "verificationMethod": [
        {
            "id": "string",
            "type": "string",
            "controller": "string",
            "publicKeyMultibase": "string"
        }
    ]
}'
```

**Path parameters**

* `tenantId`: _**\[string]**_ tenant on which to create the did.

****\
**Body paramters**\
****Did Document

```
{
    "@context": "string",
    "id": "string",
    "controller": ["string"],
    "authentication": ["string"],
    "verificationMethod": [
        {
            "id": "string",
            "type": "string",
            "controller": "string",
            "publicKeyMultibase": "string"
        }
    ]
}
```

* `@context`: _**\[String]**_ Defines the context for interpreting the DID document. Example: "[https://w3id.org/did-resolution/v1](https://w3id.org/did-resolution/v1)"
* `id`: _**\[String]**_ The unique identifier of the DID subject. Example: "did:key:z3XffJBaKvAqi2RL"
* `controller`: _**\[Array of Strings]**_ Lists the DIDs that have authority to make changes to the DID document. Example: \["did:key:z3XffJBaKvAqi2RL"]
* `authentication`: _**\[Array of Strings]**_ Lists the verification methods used for authenticating the DID subject. Example: \["did:key:z3XffJBaKvAqi2RL#key-1"]
*   `verificationMethod`: _**\[Array of Objects]**_ Contains the verification methods associated with the DID. The object consists of the following attributes:

    a. `id`: _**\[String]**_ The identifier of the verification method. Example: "did:key:z3XffJBaKvAqi2RL#key-1"

    b. `type`: _**\[String]**_ The type of the verification method. Example: "Ed25519VerificationKey2020"

    c. `controller`: _**\[String]**_ The DID that has authority to use this verification method. Example: "did:key:z3XffJBaKvAqi2RL"

    d. `publicKeyMultibase`: _**\[String]**_ The public key itself, encoded using multibase encoding. Example: "z3XffJBaKvAqi2RLLroggoq1MJW3Dy7NP4DYJuFqFjdyF"

\


**Example**

```bash
curl -X 'POST' \
  'http://localhost:8080/issuer-api/default/config/did/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "@context": "https://w3id.org/did-resolution/v1",
    "id": "did:key:z3XffJBaKvAqi2RL",
    "controller": ["did:key:z3XffJBaKvAqi2RL"],
    "authentication": ["did:key:z3XffJBaKvAqi2RL#key-1"],
    "verificationMethod": [
        {
            "id": "did:key:z3XffJBaKvAqi2RL#key-1",
            "type": "Ed25519VerificationKey2020",
            "controller": "did:key:z3XffJBaKvAqi2RL",
            "publicKeyMultibase": "z3XffJBaKvAqi2RLLroggoq1MJW3Dy7NP4DYJuFqFjdyF"
        }
    ]
}'
```
{% endtab %}

{% tab title="CLI" %}
Using the imported key, we can now import the DID.

```
config --as-issuer default did import -f {{filePath}} -k {{keyId}}
```

**Flags**

* `--as-issuer | -i`  - The config command let's you define the context in which you want to execute the command, by specifiying the arguments _--as-issuer_, _--as-verifier_ or _--as-user \[userID]_ or their shortcuts _-i_, _-v_, _-u \[userID]_
* `--file | -f` - path to the DID document file.
* `--key-id | -k` - Specifies the importated key by it's id\


**Variables**

* `filePath` - path to the DID document file.
* `keyId` - Id of the key\


**Example Command**

```
config --as-issuer default did import -f myDid.json -k 259282edee7858a54cf59ca04bca1a37cc00cf332c77254b3f98828afc8acdbe
```

\
myDid.json

```json
{
    "@context": "https://w3id.org/did-resolution/v1",
    "id": "did:key:z3XffJBaKvAqi2RL",
    "controller": ["did:key:z3XffJBaKvAqi2RL"],
    "authentication": ["did:key:z3XffJBaKvAqi2RL#key-1"],
    "verificationMethod": [
        {
            "id": "did:key:z3XffJBaKvAqi2RL#key-1",
            "type": "Ed25519VerificationKey2020",
            "controller": "did:key:z3XffJBaKvAqi2RL",
            "publicKeyMultibase": "z3XffJBaKvAqi2RLLroggoq1MJW3Dy7NP4DYJuFqFjdyF"
        }
    ]
}
```

{% hint style="info" %}
Note that the public key is encoded in "publicKeyMultibase".
{% endhint %}
{% endtab %}
{% endtabs %}

[^1]: The SSI-Kit, used by the Wallet-Kit, brings essential features needed for SSI use-cases, such as key handling and VCs.
