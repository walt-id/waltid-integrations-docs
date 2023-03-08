# Credential issuance API

Issuance is very simple, in fact, you only need to call a single HTTP POST endpoint:

## Request

POST `/issuer-api/{tenantId}/credentials/issuance/request?isPreAuthorized=true&walletId=$walletId`

```json
{
    "credentials": [
        {
        "credentialData": {
            "my data": "..."
        },
        "type": "string"
        }
    ]
}
```
e.g.:
```json
{
    "credentials": [
        {
        "credentialData": {
            "credentialSubject": {
                "currentAddress":["1 Boulevard de la Liberté, 59800 Lille"],"dateOfBirth":"1993-04-08","familyName":"DOE","firstName":"Jane","gender":"FEMALE","id":"did:ebsi:2AEMAqXWKYMu1JHPAgGcga4dxu7ThgfgN95VyJBJGZbSJUtp","nameAndFamilyNameAtBirth":"Jane DOE","personalIdentifier":"0904008084H","placeOfBirth":"LILLE, FRANCE"}
        },
        "type": "VerifiableId"
        }
    ]
}
```