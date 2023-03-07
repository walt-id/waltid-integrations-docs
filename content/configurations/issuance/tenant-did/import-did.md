# DID import

## Command Line Interface
Using the now imported key, we can import the DID. We will specify the related KeyId with the `-k` argument:

    config --as-issuer default did import -f did-key.json -k 259282edee7858a54cf59ca04bca1a37cc00cf332c77254b3f98828afc8acdbe

For reference, this is how such a DID file looks like:

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
Note that the public key is encoded in "publicKeyMultibase".

## REST API

The default _tenantId_ is "default".

For configuring the steps seen above using the REST API,
please view the
- [Issuer API Decentralized Identifier endpoint](https://wallet.walt-test.cloud/api/swagger#/Decentralized%20Identifiers)

#### To import a DID
- use `POST /issuer-api/{tenantId}/config/did/import`, with the DID document as body