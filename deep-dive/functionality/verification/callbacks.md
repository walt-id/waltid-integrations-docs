# Verification callbacks

As seen in the first example, you can optionally set a callback:

```https://wallet.walt-test.cloud/verifier-api/default/present?walletId=walt.id&vcType=VerifiableId&verificationCallbackUrl=http://wallet.local:5555/callback/5dd9f971-9cd2-4c41-a40f-5340ac6d1fd3```
(Note `&verificationCallbackUrl=`)

When setting a callback, the Wallet Kit will then call this callback as webhook when the user shares a credential (in
the walt.id demo wallet: actually clicks "Share credentials").

Before answering the user, the Wallet Kit will send out an HTTP Post request using the parameters described below.

- When the callback answers HTTP statuses
    - Statuses:
        - OK (200),
        - NoContent (201),
        - or Accepted (202)
    - the Wallet Kit will mark the callback as accepted and continue its normal operation.

---

- When the callback answers HTTP statuses
    - Statuses:
        - MovedPermanently (301),
        - Found (302),
        - TemporaryRedirect (307),
        - or PermanentRedirect (308)
    - the Wallet Kit will abort its operation and redirect the user (using the `Location` header) to the `Location`
      specified by the callback.
    - This is useful for redirecting to pages _based_ on what credentials the user shares or change depending on the
      data of the credentials.

---

- When the callback answers HTTP statuses
    - Statuses:
        - Unauthorized (401),
        - or Forbidden (403)
    - the Wallet Kit will invalidate the status and set overallValid to false, even if the selected `VerificationPolicy`
      s would result in an `overallValid = true`.

## Callback data to work with

When you set up your webhook to listen for such a Wallet Kit callback, you have a variety of data to work with:

- state: (UUID) ID of the verification session
- subject: (DID) DID of the user that created the shared presentation
- auth_token: (JWT[Subject]) Signed representation of subject = DID
- vps: (List[VPVerificationResult])
    - VPVerificationResult:
        - vp: (JWT) Signed representation of the Verifiable Presentation
            - Including DIDs, issuance dates (attribute `iat`, `nbf`), etc...
            - and obviously the actual Verifiable Credential (in attribute `vc`)
        - vcs: (List[JWT])
            - Signed Verifiable Credentials sourced from the Verifiable Presentation (VC in attribute `vc`, issuance
              date `iat` `nbf`, Subject DID `sub`, ...)
        - verification_result: (VerificationResult)
            - valid: Boolean
                - overall valid state
            - policyResults: Map[Policy -> Boolean]
                - e.g. `policyResults={SignaturePolicy=true, ChallengePolicy=true, PresentationDefinitionPolicy=true}`

### Example JSON body you'll receive with a webhook callback for the VerifiableID demo

```json
{
  "isValid": true,
  "state": "41676715-a069-4f43-baee-57bdbeaf2c98",
  "subject": "did:key:z6Mkidk54UoPVhPqkWExngRj3Cd33jAdNcKfd6ePkrCZEbjU",
  "vps": [
    {
      "vcs": [
        {
          "context": [
            {
              "_isObject": false,
              "properties": {},
              "uri": "https://www.w3.org/2018/credentials/v1"
            }
          ],
          "credentialSchema": {
            "id": "https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba",
            "properties": {
              "id": "https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba"
            },
            "type": "FullJsonSchemaValidator2021"
          },
          "credentialSubject": {
            "id": "did:key:z6Mkidk54UoPVhPqkWExngRj3Cd33jAdNcKfd6ePkrCZEbjU",
            "properties": {
              "currentAddress": [
                "1 Boulevard de la Liberté, 59800 Lille"
              ],
              "dateOfBirth": "1993-04-08",
              "familyName": "DOE",
              "firstName": "Jane",
              "gender": "FEMALE",
              "nameAndFamilyNameAtBirth": "Jane DOE",
              "personalIdentifier": "0904008084H",
              "placeOfBirth": "LILLE, FRANCE"
            }
          },
          "id": "urn:uuid:7cf18a60-e624-44b0-8ea8-aec630a2fb66",
          "issuanceDate": "2023-01-09T15:41:50Z",
          "issued": "2023-01-09T15:41:50Z",
          "issuer": {
            "_isObject": false,
            "id": "did:key:z6Mkvrfpsv1pB3qwEXJAWtz6u7zgib2PZYj5zRg8gJfCsJqv",
            "properties": {}
          },
          "issuerId": "did:key:z6Mkvrfpsv1pB3qwEXJAWtz6u7zgib2PZYj5zRg8gJfCsJqv",
          "jwt": "eyJraWQiOiJkaWQ6a2V5Ono2TWt2cmZwc3YxcEIzcXdFWEpBV3R6NnU3emdpYjJQWllqNXpSZzhnSmZDc0pxdiN6Nk1rdnJmcHN2MXBCM3F3RVhKQVd0ejZ1N3pnaWIyUFpZajV6Umc4Z0pmQ3NKcXYiLCJ0eXAiOiJKV1QiLCJhbGciOiJFZERTQSJ9.eyJzdWIiOiJkaWQ6a2V5Ono2TWtpZGs1NFVvUFZoUHFrV0V4bmdSajNDZDMzakFkTmNLZmQ2ZVBrckNaRWJqVSIsIm5iZiI6MTY3MzI3ODkxMCwiaXNzIjoiZGlkOmtleTp6Nk1rdnJmcHN2MXBCM3F3RVhKQVd0ejZ1N3pnaWIyUFpZajV6Umc4Z0pmQ3NKcXYiLCJpYXQiOjE2NzMyNzg5MTAsInZjIjp7InR5cGUiOlsiVmVyaWZpYWJsZUNyZWRlbnRpYWwiLCJWZXJpZmlhYmxlQXR0ZXN0YXRpb24iLCJWZXJpZmlhYmxlSWQiXSwiQGNvbnRleHQiOlsiaHR0cHM6Ly93d3cudzMub3JnLzIwMTgvY3JlZGVudGlhbHMvdjEiXSwiaWQiOiJ1cm46dXVpZDo3Y2YxOGE2MC1lNjI0LTQ0YjAtOGVhOC1hZWM2MzBhMmZiNjYiLCJpc3N1ZXIiOiJkaWQ6a2V5Ono2TWt2cmZwc3YxcEIzcXdFWEpBV3R6NnU3emdpYjJQWllqNXpSZzhnSmZDc0pxdiIsImlzc3VhbmNlRGF0ZSI6IjIwMjMtMDEtMDlUMTU6NDE6NTBaIiwiaXNzdWVkIjoiMjAyMy0wMS0wOVQxNTo0MTo1MFoiLCJ2YWxpZEZyb20iOiIyMDIzLTAxLTA5VDE1OjQxOjUwWiIsImNyZWRlbnRpYWxTY2hlbWEiOnsiaWQiOiJodHRwczovL2FwaS5wcmVwcm9kLmVic2kuZXUvdHJ1c3RlZC1zY2hlbWFzLXJlZ2lzdHJ5L3YxL3NjaGVtYXMvMHhiNzdmODUxNmE5NjU2MzFiNGYxOTdhZDU0YzY1YTllMmY5OTM2ZWJmYjc2YmFlNDkwNmQzMzc0NGRiY2M2MGJhIiwidHlwZSI6IkZ1bGxKc29uU2NoZW1hVmFsaWRhdG9yMjAyMSJ9LCJjcmVkZW50aWFsU3ViamVjdCI6eyJpZCI6ImRpZDprZXk6ejZNa2lkazU0VW9QVmhQcWtXRXhuZ1JqM0NkMzNqQWROY0tmZDZlUGtyQ1pFYmpVIiwiY3VycmVudEFkZHJlc3MiOlsiMSBCb3VsZXZhcmQgZGUgbGEgTGliZXJ0w6ksIDU5ODAwIExpbGxlIl0sImRhdGVPZkJpcnRoIjoiMTk5My0wNC0wOCIsImZhbWlseU5hbWUiOiJET0UiLCJmaXJzdE5hbWUiOiJKYW5lIiwiZ2VuZGVyIjoiRkVNQUxFIiwibmFtZUFuZEZhbWlseU5hbWVBdEJpcnRoIjoiSmFuZSBET0UiLCJwZXJzb25hbElkZW50aWZpZXIiOiIwOTA0MDA4MDg0SCIsInBsYWNlT2ZCaXJ0aCI6IkxJTExFLCBGUkFOQ0UifSwiZXZpZGVuY2UiOlt7ImRvY3VtZW50UHJlc2VuY2UiOlsiUGh5c2ljYWwiXSwiZXZpZGVuY2VEb2N1bWVudCI6WyJQYXNzcG9ydCJdLCJzdWJqZWN0UHJlc2VuY2UiOiJQaHlzaWNhbCIsInR5cGUiOlsiRG9jdW1lbnRWZXJpZmljYXRpb24iXSwidmVyaWZpZXIiOiJkaWQ6ZWJzaToyQTlCWjlTVWU2QmF0YWNTcHZzMVY1Q2RqSHZMcFE3YkVzaTJKYjZMZEhLblF4YU4ifV19LCJqdGkiOiJ1cm46dXVpZDo3Y2YxOGE2MC1lNjI0LTQ0YjAtOGVhOC1hZWM2MzBhMmZiNjYifQ.no9qGLBMSR1tq9Svn0fNdI5B0gIlO6NrwQrnvd7tqVjnPdXvpeTR4E9TtI346Ba6YQllbrSh9-HFIa-uzDlzBA",
          "properties": {
            "evidence": [
              {
                "documentPresence": [
                  "Physical"
                ],
                "evidenceDocument": [
                  "Passport"
                ],
                "subjectPresence": "Physical",
                "type": [
                  "DocumentVerification"
                ],
                "verifier": "did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN"
              }
            ]
          },
          "subjectId": "did:key:z6Mkidk54UoPVhPqkWExngRj3Cd33jAdNcKfd6ePkrCZEbjU",
          "type": [
            "VerifiableCredential",
            "VerifiableAttestation",
            "VerifiableId"
          ],
          "validFrom": "2023-01-09T15:41:50Z"
        }
      ],
      "verification_result": {
        "policyResults": {
          "SignaturePolicy": true,
          "ChallengePolicy": true,
          "PresentationDefinitionPolicy": true
        },
        "valid": true
      },
      "vp": {
        "holder": "did:key:z6Mkidk54UoPVhPqkWExngRj3Cd33jAdNcKfd6ePkrCZEbjU",
        "issuerId": "did:key:z6Mkidk54UoPVhPqkWExngRj3Cd33jAdNcKfd6ePkrCZEbjU",
        "subjectId": "did:key:z6Mkidk54UoPVhPqkWExngRj3Cd33jAdNcKfd6ePkrCZEbjU",
        "verifiableCredential": [
          {
            "context": [
              {
                "_isObject": false,
                "properties": {},
                "uri": "https://www.w3.org/2018/credentials/v1"
              }
            ],
            "credentialSchema": {
              "id": "https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba",
              "properties": {
                "id": "https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba"
              },
              "type": "FullJsonSchemaValidator2021"
            },
            "credentialSubject": {
              "id": "did:key:z6Mkidk54UoPVhPqkWExngRj3Cd33jAdNcKfd6ePkrCZEbjU",
              "properties": {
                "currentAddress": [
                  "1 Boulevard de la Liberté, 59800 Lille"
                ],
                "dateOfBirth": "1993-04-08",
                "familyName": "DOE",
                "firstName": "Jane",
                "gender": "FEMALE",
                "nameAndFamilyNameAtBirth": "Jane DOE",
                "personalIdentifier": "0904008084H",
                "placeOfBirth": "LILLE, FRANCE"
              }
            },
            "id": "urn:uuid:7cf18a60-e624-44b0-8ea8-aec630a2fb66",
            "issuanceDate": "2023-01-09T15:41:50Z",
            "issued": "2023-01-09T15:41:50Z",
            "issuer": {
              "_isObject": false,
              "id": "did:key:z6Mkvrfpsv1pB3qwEXJAWtz6u7zgib2PZYj5zRg8gJfCsJqv",
              "properties": {}
            },
            "issuerId": "did:key:z6Mkvrfpsv1pB3qwEXJAWtz6u7zgib2PZYj5zRg8gJfCsJqv",
            "jwt": "eyJraWQiOiJkaWQ6a2V5Ono2TWt2cmZwc3YxcEIzcXdFWEpBV3R6NnU3emdpYjJQWllqNXpSZzhnSmZDc0pxdiN6Nk1rdnJmcHN2MXBCM3F3RVhKQVd0ejZ1N3pnaWIyUFpZajV6Umc4Z0pmQ3NKcXYiLCJ0eXAiOiJKV1QiLCJhbGciOiJFZERTQSJ9.eyJzdWIiOiJkaWQ6a2V5Ono2TWtpZGs1NFVvUFZoUHFrV0V4bmdSajNDZDMzakFkTmNLZmQ2ZVBrckNaRWJqVSIsIm5iZiI6MTY3MzI3ODkxMCwiaXNzIjoiZGlkOmtleTp6Nk1rdnJmcHN2MXBCM3F3RVhKQVd0ejZ1N3pnaWIyUFpZajV6Umc4Z0pmQ3NKcXYiLCJpYXQiOjE2NzMyNzg5MTAsInZjIjp7InR5cGUiOlsiVmVyaWZpYWJsZUNyZWRlbnRpYWwiLCJWZXJpZmlhYmxlQXR0ZXN0YXRpb24iLCJWZXJpZmlhYmxlSWQiXSwiQGNvbnRleHQiOlsiaHR0cHM6Ly93d3cudzMub3JnLzIwMTgvY3JlZGVudGlhbHMvdjEiXSwiaWQiOiJ1cm46dXVpZDo3Y2YxOGE2MC1lNjI0LTQ0YjAtOGVhOC1hZWM2MzBhMmZiNjYiLCJpc3N1ZXIiOiJkaWQ6a2V5Ono2TWt2cmZwc3YxcEIzcXdFWEpBV3R6NnU3emdpYjJQWllqNXpSZzhnSmZDc0pxdiIsImlzc3VhbmNlRGF0ZSI6IjIwMjMtMDEtMDlUMTU6NDE6NTBaIiwiaXNzdWVkIjoiMjAyMy0wMS0wOVQxNTo0MTo1MFoiLCJ2YWxpZEZyb20iOiIyMDIzLTAxLTA5VDE1OjQxOjUwWiIsImNyZWRlbnRpYWxTY2hlbWEiOnsiaWQiOiJodHRwczovL2FwaS5wcmVwcm9kLmVic2kuZXUvdHJ1c3RlZC1zY2hlbWFzLXJlZ2lzdHJ5L3YxL3NjaGVtYXMvMHhiNzdmODUxNmE5NjU2MzFiNGYxOTdhZDU0YzY1YTllMmY5OTM2ZWJmYjc2YmFlNDkwNmQzMzc0NGRiY2M2MGJhIiwidHlwZSI6IkZ1bGxKc29uU2NoZW1hVmFsaWRhdG9yMjAyMSJ9LCJjcmVkZW50aWFsU3ViamVjdCI6eyJpZCI6ImRpZDprZXk6ejZNa2lkazU0VW9QVmhQcWtXRXhuZ1JqM0NkMzNqQWROY0tmZDZlUGtyQ1pFYmpVIiwiY3VycmVudEFkZHJlc3MiOlsiMSBCb3VsZXZhcmQgZGUgbGEgTGliZXJ0w6ksIDU5ODAwIExpbGxlIl0sImRhdGVPZkJpcnRoIjoiMTk5My0wNC0wOCIsImZhbWlseU5hbWUiOiJET0UiLCJmaXJzdE5hbWUiOiJKYW5lIiwiZ2VuZGVyIjoiRkVNQUxFIiwibmFtZUFuZEZhbWlseU5hbWVBdEJpcnRoIjoiSmFuZSBET0UiLCJwZXJzb25hbElkZW50aWZpZXIiOiIwOTA0MDA4MDg0SCIsInBsYWNlT2ZCaXJ0aCI6IkxJTExFLCBGUkFOQ0UifSwiZXZpZGVuY2UiOlt7ImRvY3VtZW50UHJlc2VuY2UiOlsiUGh5c2ljYWwiXSwiZXZpZGVuY2VEb2N1bWVudCI6WyJQYXNzcG9ydCJdLCJzdWJqZWN0UHJlc2VuY2UiOiJQaHlzaWNhbCIsInR5cGUiOlsiRG9jdW1lbnRWZXJpZmljYXRpb24iXSwidmVyaWZpZXIiOiJkaWQ6ZWJzaToyQTlCWjlTVWU2QmF0YWNTcHZzMVY1Q2RqSHZMcFE3YkVzaTJKYjZMZEhLblF4YU4ifV19LCJqdGkiOiJ1cm46dXVpZDo3Y2YxOGE2MC1lNjI0LTQ0YjAtOGVhOC1hZWM2MzBhMmZiNjYifQ.no9qGLBMSR1tq9Svn0fNdI5B0gIlO6NrwQrnvd7tqVjnPdXvpeTR4E9TtI346Ba6YQllbrSh9-HFIa-uzDlzBA",
            "properties": {
              "evidence": [
                {
                  "documentPresence": [
                    "Physical"
                  ],
                  "evidenceDocument": [
                    "Passport"
                  ],
                  "subjectPresence": "Physical",
                  "type": [
                    "DocumentVerification"
                  ],
                  "verifier": "did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN"
                }
              ]
            },
            "subjectId": "did:key:z6Mkidk54UoPVhPqkWExngRj3Cd33jAdNcKfd6ePkrCZEbjU",
            "type": [
              "VerifiableCredential",
              "VerifiableAttestation",
              "VerifiableId"
            ],
            "validFrom": "2023-01-09T15:41:50Z"
          }
        ],
        "challenge": "41676715-a069-4f43-baee-57bdbeaf2c98",
        "context": [
          {
            "_isObject": false,
            "properties": {},
            "uri": "https://www.w3.org/2018/credentials/v1"
          }
        ],
        "id": "urn:uuid:a8d3b6fb-03ca-4550-8a95-f812d4ee8f8f",
        "jwt": "eyJraWQiOiJkaWQ6a2V5Ono2TWtpZGs1NFVvUFZoUHFrV0V4bmdSajNDZDMzakFkTmNLZmQ2ZVBrckNaRWJqVSN6Nk1raWRrNTRVb1BWaFBxa1dFeG5nUmozQ2QzM2pBZE5jS2ZkNmVQa3JDWkVialUiLCJ0eXAiOiJKV1QiLCJhbGciOiJFZERTQSJ9.eyJzdWIiOiJkaWQ6a2V5Ono2TWtpZGs1NFVvUFZoUHFrV0V4bmdSajNDZDMzakFkTmNLZmQ2ZVBrckNaRWJqVSIsIm5iZiI6MTY3NDA4Nzc2MCwiaXNzIjoiZGlkOmtleTp6Nk1raWRrNTRVb1BWaFBxa1dFeG5nUmozQ2QzM2pBZE5jS2ZkNmVQa3JDWkVialUiLCJ2cCI6eyJ0eXBlIjpbIlZlcmlmaWFibGVQcmVzZW50YXRpb24iXSwiQGNvbnRleHQiOlsiaHR0cHM6Ly93d3cudzMub3JnLzIwMTgvY3JlZGVudGlhbHMvdjEiXSwiaWQiOiJ1cm46dXVpZDphOGQzYjZmYi0wM2NhLTQ1NTAtOGE5NS1mODEyZDRlZThmOGYiLCJob2xkZXIiOiJkaWQ6a2V5Ono2TWtpZGs1NFVvUFZoUHFrV0V4bmdSajNDZDMzakFkTmNLZmQ2ZVBrckNaRWJqVSIsInZlcmlmaWFibGVDcmVkZW50aWFsIjpbImV5SnJhV1FpT2lKa2FXUTZhMlY1T25vMlRXdDJjbVp3YzNZeGNFSXpjWGRGV0VwQlYzUjZOblUzZW1kcFlqSlFXbGxxTlhwU1p6aG5TbVpEYzBweGRpTjZOazFyZG5KbWNITjJNWEJDTTNGM1JWaEtRVmQwZWpaMU4zcG5hV0l5VUZwWmFqVjZVbWM0WjBwbVEzTktjWFlpTENKMGVYQWlPaUpLVjFRaUxDSmhiR2NpT2lKRlpFUlRRU0o5LmV5SnpkV0lpT2lKa2FXUTZhMlY1T25vMlRXdHBaR3MxTkZWdlVGWm9VSEZyVjBWNGJtZFNhak5EWkRNemFrRmtUbU5MWm1RMlpWQnJja05hUldKcVZTSXNJbTVpWmlJNk1UWTNNekkzT0RreE1Dd2lhWE56SWpvaVpHbGtPbXRsZVRwNk5rMXJkbkptY0hOMk1YQkNNM0YzUlZoS1FWZDBlaloxTjNwbmFXSXlVRnBaYWpWNlVtYzRaMHBtUTNOS2NYWWlMQ0pwWVhRaU9qRTJOek15TnpnNU1UQXNJblpqSWpwN0luUjVjR1VpT2xzaVZtVnlhV1pwWVdKc1pVTnlaV1JsYm5ScFlXd2lMQ0pXWlhKcFptbGhZbXhsUVhSMFpYTjBZWFJwYjI0aUxDSldaWEpwWm1saFlteGxTV1FpWFN3aVFHTnZiblJsZUhRaU9sc2lhSFIwY0hNNkx5OTNkM2N1ZHpNdWIzSm5Mekl3TVRndlkzSmxaR1Z1ZEdsaGJITXZkakVpWFN3aWFXUWlPaUoxY200NmRYVnBaRG8zWTJZeE9HRTJNQzFsTmpJMExUUTBZakF0T0dWaE9DMWhaV00yTXpCaE1tWmlOallpTENKcGMzTjFaWElpT2lKa2FXUTZhMlY1T25vMlRXdDJjbVp3YzNZeGNFSXpjWGRGV0VwQlYzUjZOblUzZW1kcFlqSlFXbGxxTlhwU1p6aG5TbVpEYzBweGRpSXNJbWx6YzNWaGJtTmxSR0YwWlNJNklqSXdNak10TURFdE1EbFVNVFU2TkRFNk5UQmFJaXdpYVhOemRXVmtJam9pTWpBeU15MHdNUzB3T1ZReE5UbzBNVG8xTUZvaUxDSjJZV3hwWkVaeWIyMGlPaUl5TURJekxUQXhMVEE1VkRFMU9qUXhPalV3V2lJc0ltTnlaV1JsYm5ScFlXeFRZMmhsYldFaU9uc2lhV1FpT2lKb2RIUndjem92TDJGd2FTNXdjbVZ3Y205a0xtVmljMmt1WlhVdmRISjFjM1JsWkMxelkyaGxiV0Z6TFhKbFoybHpkSEo1TDNZeEwzTmphR1Z0WVhNdk1IaGlOemRtT0RVeE5tRTVOalUyTXpGaU5HWXhPVGRoWkRVMFl6WTFZVGxsTW1ZNU9UTTJaV0ptWWpjMlltRmxORGt3Tm1Rek16YzBOR1JpWTJNMk1HSmhJaXdpZEhsd1pTSTZJa1oxYkd4S2MyOXVVMk5vWlcxaFZtRnNhV1JoZEc5eU1qQXlNU0o5TENKamNtVmtaVzUwYVdGc1UzVmlhbVZqZENJNmV5SnBaQ0k2SW1ScFpEcHJaWGs2ZWpaTmEybGthelUwVlc5UVZtaFFjV3RYUlhodVoxSnFNME5rTXpOcVFXUk9ZMHRtWkRabFVHdHlRMXBGWW1wVklpd2lZM1Z5Y21WdWRFRmtaSEpsYzNNaU9sc2lNU0JDYjNWc1pYWmhjbVFnWkdVZ2JHRWdUR2xpWlhKMHc2a3NJRFU1T0RBd0lFeHBiR3hsSWwwc0ltUmhkR1ZQWmtKcGNuUm9Jam9pTVRrNU15MHdOQzB3T0NJc0ltWmhiV2xzZVU1aGJXVWlPaUpFVDBVaUxDSm1hWEp6ZEU1aGJXVWlPaUpLWVc1bElpd2laMlZ1WkdWeUlqb2lSa1ZOUVV4Rklpd2libUZ0WlVGdVpFWmhiV2xzZVU1aGJXVkJkRUpwY25Sb0lqb2lTbUZ1WlNCRVQwVWlMQ0p3WlhKemIyNWhiRWxrWlc1MGFXWnBaWElpT2lJd09UQTBNREE0TURnMFNDSXNJbkJzWVdObFQyWkNhWEowYUNJNklreEpURXhGTENCR1VrRk9RMFVpZlN3aVpYWnBaR1Z1WTJVaU9sdDdJbVJ2WTNWdFpXNTBVSEpsYzJWdVkyVWlPbHNpVUdoNWMybGpZV3dpWFN3aVpYWnBaR1Z1WTJWRWIyTjFiV1Z1ZENJNld5SlFZWE56Y0c5eWRDSmRMQ0p6ZFdKcVpXTjBVSEpsYzJWdVkyVWlPaUpRYUhsemFXTmhiQ0lzSW5SNWNHVWlPbHNpUkc5amRXMWxiblJXWlhKcFptbGpZWFJwYjI0aVhTd2lkbVZ5YVdacFpYSWlPaUprYVdRNlpXSnphVG95UVRsQ1dqbFRWV1UyUW1GMFlXTlRjSFp6TVZZMVEyUnFTSFpNY0ZFM1lrVnphVEpLWWpaTVpFaExibEY0WVU0aWZWMTlMQ0pxZEdraU9pSjFjbTQ2ZFhWcFpEbzNZMll4T0dFMk1DMWxOakkwTFRRMFlqQXRPR1ZoT0MxaFpXTTJNekJoTW1aaU5qWWlmUS5ubzlxR0xCTVNSMXRxOVN2bjBmTmRJNUIwZ0lsTzZOcndRcm52ZDd0cVZqblBkWHZwZVRSNEU5VHRJMzQ2QmE2WVFsbGJyU2g5LUhGSWEtdXpEbHpCQSJdfSwiaWF0IjoxNjc0MDg3NzYwLCJub25jZSI6IjQxNjc2NzE1LWEwNjktNGY0My1iYWVlLTU3YmRiZWFmMmM5OCIsImp0aSI6InVybjp1dWlkOmE4ZDNiNmZiLTAzY2EtNDU1MC04YTk1LWY4MTJkNGVlOGY4ZiJ9.RxFMgwvyTQkny0eCF2my016ff9yU3sUC8oOHARKRYMG7-u0He8sjjwB7cM0qIxVuNUbXfqAGm79UXIZGX4MzAg",
        "properties": {
          "holder": "did:key:z6Mkidk54UoPVhPqkWExngRj3Cd33jAdNcKfd6ePkrCZEbjU",
          "verifiableCredential": [
            "eyJraWQiOiJkaWQ6a2V5Ono2TWt2cmZwc3YxcEIzcXdFWEpBV3R6NnU3emdpYjJQWllqNXpSZzhnSmZDc0pxdiN6Nk1rdnJmcHN2MXBCM3F3RVhKQVd0ejZ1N3pnaWIyUFpZajV6Umc4Z0pmQ3NKcXYiLCJ0eXAiOiJKV1QiLCJhbGciOiJFZERTQSJ9.eyJzdWIiOiJkaWQ6a2V5Ono2TWtpZGs1NFVvUFZoUHFrV0V4bmdSajNDZDMzakFkTmNLZmQ2ZVBrckNaRWJqVSIsIm5iZiI6MTY3MzI3ODkxMCwiaXNzIjoiZGlkOmtleTp6Nk1rdnJmcHN2MXBCM3F3RVhKQVd0ejZ1N3pnaWIyUFpZajV6Umc4Z0pmQ3NKcXYiLCJpYXQiOjE2NzMyNzg5MTAsInZjIjp7InR5cGUiOlsiVmVyaWZpYWJsZUNyZWRlbnRpYWwiLCJWZXJpZmlhYmxlQXR0ZXN0YXRpb24iLCJWZXJpZmlhYmxlSWQiXSwiQGNvbnRleHQiOlsiaHR0cHM6Ly93d3cudzMub3JnLzIwMTgvY3JlZGVudGlhbHMvdjEiXSwiaWQiOiJ1cm46dXVpZDo3Y2YxOGE2MC1lNjI0LTQ0YjAtOGVhOC1hZWM2MzBhMmZiNjYiLCJpc3N1ZXIiOiJkaWQ6a2V5Ono2TWt2cmZwc3YxcEIzcXdFWEpBV3R6NnU3emdpYjJQWllqNXpSZzhnSmZDc0pxdiIsImlzc3VhbmNlRGF0ZSI6IjIwMjMtMDEtMDlUMTU6NDE6NTBaIiwiaXNzdWVkIjoiMjAyMy0wMS0wOVQxNTo0MTo1MFoiLCJ2YWxpZEZyb20iOiIyMDIzLTAxLTA5VDE1OjQxOjUwWiIsImNyZWRlbnRpYWxTY2hlbWEiOnsiaWQiOiJodHRwczovL2FwaS5wcmVwcm9kLmVic2kuZXUvdHJ1c3RlZC1zY2hlbWFzLXJlZ2lzdHJ5L3YxL3NjaGVtYXMvMHhiNzdmODUxNmE5NjU2MzFiNGYxOTdhZDU0YzY1YTllMmY5OTM2ZWJmYjc2YmFlNDkwNmQzMzc0NGRiY2M2MGJhIiwidHlwZSI6IkZ1bGxKc29uU2NoZW1hVmFsaWRhdG9yMjAyMSJ9LCJjcmVkZW50aWFsU3ViamVjdCI6eyJpZCI6ImRpZDprZXk6ejZNa2lkazU0VW9QVmhQcWtXRXhuZ1JqM0NkMzNqQWROY0tmZDZlUGtyQ1pFYmpVIiwiY3VycmVudEFkZHJlc3MiOlsiMSBCb3VsZXZhcmQgZGUgbGEgTGliZXJ0w6ksIDU5ODAwIExpbGxlIl0sImRhdGVPZkJpcnRoIjoiMTk5My0wNC0wOCIsImZhbWlseU5hbWUiOiJET0UiLCJmaXJzdE5hbWUiOiJKYW5lIiwiZ2VuZGVyIjoiRkVNQUxFIiwibmFtZUFuZEZhbWlseU5hbWVBdEJpcnRoIjoiSmFuZSBET0UiLCJwZXJzb25hbElkZW50aWZpZXIiOiIwOTA0MDA4MDg0SCIsInBsYWNlT2ZCaXJ0aCI6IkxJTExFLCBGUkFOQ0UifSwiZXZpZGVuY2UiOlt7ImRvY3VtZW50UHJlc2VuY2UiOlsiUGh5c2ljYWwiXSwiZXZpZGVuY2VEb2N1bWVudCI6WyJQYXNzcG9ydCJdLCJzdWJqZWN0UHJlc2VuY2UiOiJQaHlzaWNhbCIsInR5cGUiOlsiRG9jdW1lbnRWZXJpZmljYXRpb24iXSwidmVyaWZpZXIiOiJkaWQ6ZWJzaToyQTlCWjlTVWU2QmF0YWNTcHZzMVY1Q2RqSHZMcFE3YkVzaTJKYjZMZEhLblF4YU4ifV19LCJqdGkiOiJ1cm46dXVpZDo3Y2YxOGE2MC1lNjI0LTQ0YjAtOGVhOC1hZWM2MzBhMmZiNjYifQ.no9qGLBMSR1tq9Svn0fNdI5B0gIlO6NrwQrnvd7tqVjnPdXvpeTR4E9TtI346Ba6YQllbrSh9-HFIa-uzDlzBA"
          ]
        },
        "type": [
          "VerifiablePresentation"
        ]
      }
    }
  ]
}
```

(Empty values that are not set [= null] are omitted for this example, e.g. no expirationDate was set, thus you'll
receive `"expirationDate": null`)