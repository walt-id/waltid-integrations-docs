# Key import

## Command Line Interface

First, import your keypair from e.g. veramo in JWK or PEM format. JWK is preferred:

    config --as-issuer default key import key.jwk.json

For reference, this is how such a JWK keypair looks like:

```json
{
  "kty": "OKP",
  "d": "SKNkmI0Fs2vyo7owHQMRzC9OqhACmPadD-tsAv4HQ3M",
  "use": "sig",
  "crv": "Ed25519",
  "kid": "259282edee7858a54cf59ca04bca1a37cc00cf332c77254b3f98828afc8acdbe",
  "x": "JZKC7e54WKVM9ZygS8oaN8wAzzMsdyVLP5iCivyKzb4",
  "alg": "EdDSA"
}
```

- For key type ("kty") OKP:
    - "crv" will contain the subtype of the key (from the JSON Web Elliptic Curve registry).
    - **"x" contains the public key encoded using the base64url scheme.**
    - **"d" contains the private key encoded using the base64url scheme.**

(base64url is Base64, but 1. replaces "+" with "-", 2. replaces "/" with "_", 3. has no "=" padding, 4. has no line
seperators)

**When importing or generating a key, a KeyId will be returned.  
This KeyId will be used for the next step.**

(In this case, the KeyId in the JWK "keyId" field will be used.)

## REST API

For configuring the steps seen above using the REST API,
please view the

- [Issuer API Key Management endpoint](https://wallet.walt-test.cloud/api/swagger#/Key%20Management)

#### To import a key
- use `POST /issuer-api/{tenantId}/config/key/import`, with the key in JWK (preferred) or PEM format as body

```shell
curl -X 'POST' \
  'https://wallet.walt-test.cloud/issuer-api/default/config/key/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '>>>the key to import<<<'