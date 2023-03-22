# Revocation of VCs

By default, the walt.id SSI Kit, which is used by the wallet-kit and therefore by the walt.id integrations, includes a variety of `VerificationPolicy`'s. To better understand how things are connected, have a look at the [Architecture section](../../architecture.md).

One of the Verification Policies is the `CredentialStatusPolicy`.

`CredentialStatus` is a simple format, it looks roughly like this:

```kotlin
@Serializable
data class CredentialStatus(
    val id: String,
    var type: String
)
```

## SimpleCredentialStatus2022

`CredentialStatusPolicy` supports `SimpleCredentialStatus2022`.

A `CredentialStatus` for `SimpleCredentialStatus2022` might look like this:

```json
{
  "credentialStatus": {
    "type": "SimpleCredentialStatus2022",
    "id": "https://revocations.credential-issuer.example.org/TESMX6WQNQCNMGX6P4DNUHWVG5YGVN23KZTWNMTALNQFW6LFZTOQ"
  }
}
```

This `credentialStatus` may be used in a Verifiable Credential but may also be embedded into other objects, e.g. ZCap-LD.
