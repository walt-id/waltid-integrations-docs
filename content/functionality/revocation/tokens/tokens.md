# Token types

A `SimpleCredentialStatus2022` contains two types of tokens:

1. Base tokens
2. Revocation tokens - **derived** (from the base token).

#### Difference between the token types

The revocation token is used to check for revocation of a credential or any other object (e.g. ZCap) using
SimpleCredentialStatus2022.
It is the publicly shared token that's e.g. embedded in the credential
The public revocation token is derived from a private base token.

The base token is private and shall not be shared.

This allows all users to validate a object like a credential for its validity (that it hasn't been revoked yet),

however only selected users, e.g. the issuer itself can actually issue the revocation (= revoke the credential again).
For this, the issuer will use the _private_ base token.

#### Definition of the token types

A base token is created by concatenating two UUID compatible strings, e.g.
`327c5c69-d1df-42d3-b8bf-9bbb49030377bd0877f2-a276-4dbe-bcd8-f3e60019610f`.

A derived token is created by:

1. Hashing the base token using SHA256
2. Creating a web URL safe Base32 representation of the hash
3. Removing any remaining web-unsafe special characters, e.g. possible padding at the end with the "=" sign.

Example code:

```kotlin
fun getRevocationToken(baseToken: String) = toBase32String(DigestUtils.sha256(baseToken)).replace("=", "")
```