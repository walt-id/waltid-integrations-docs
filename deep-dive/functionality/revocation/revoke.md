# Revoke a token

While checking a token for revocation is a public operation, actually revoking the token is a restricted operation.
To revoke a revocation token, you will need the base token that was initially generated, e.g. when issuing the
credential.

To revoke the token, you will send an HTTP POST to the same endpoint, however using the base token instead of the
revocation check token this time.

POST `http://localhost:7001/v1/revocations/327c5c69-d1df-42d3-b8bf-9bbb49030377bd0877f2-a276-4dbe-bcd8-f3e60019610f`

Example response: HTTP 201

## Optional: Not seeing that the token is revoked

GET `http://localhost:7001/v1/revocations/TESMX6WQNQCNMGX6P4DNUHWVG5YGVN23KZTWNMTALNQFW6LFZTOQ`

```json
{
  "isRevoked": true,
  "timeOfRevocation": 1674004245748,
  "token": "TESMX6WQNQCNMGX6P4DNUHWVG5YGVN23KZTWNMTALNQFW6LFZTOQ"
}
```

As you can now see, the revocation token was revoked by the request using the base token above.
See the response object description above for further information.