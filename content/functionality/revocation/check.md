# Check if a token was revoked

When wanting to validate a SimpleCredentialStatus2022 "credentialStatus" object, you would get the check URL from the
JSON:

```json
{
  "type": "SimpleCredentialStatus2022",
  "id": "https://revocations.credential-issuer.example.org/TESMX6WQNQCNMGX6P4DNUHWVG5YGVN23KZTWNMTALNQFW6LFZTOQ"
}
```

See the URL in "id" above. This URL already contains the host to contact, path to use, and revocation check token.

Then using a simple HTTP GET
request: `http://localhost:7001/v1/revocations/TESMX6WQNQCNMGX6P4DNUHWVG5YGVN23KZTWNMTALNQFW6LFZTOQ`
(a local SSI Kit URL was used above, as the URL from the JSON object is hypothetical).

Example response:

```json
{
  "isRevoked": false,
  "token": "TESMX6WQNQCNMGX6P4DNUHWVG5YGVN23KZTWNMTALNQFW6LFZTOQ"
}
```

The revocation result seen above might include any of these attributes:

```kotlin
@Serializable
data class RevocationResult(
    val token: String,
    val isRevoked: Boolean,
    @Json(serializeNull = false) val timeOfRevocation: Long? = null
)
```

1. `token` simply shows the queried token.
2. `isRevoked` is the final answer if the credential containing this specific revocation token check was revoked at this
   point in time.
3. `timeOfRevocation` is an optional attribute which is set when the credential was actually revoked. It represents date
   and time of the revocation as a UTC Unix timestamp with millisecond precision.