# Configuration

To define the voucher codes, create a CSV file with two columns: one for the voucher code and the other for the verifiable credential data.

#### CSV Format

| Voucher Code | Verifiable Credential Data |
| ------------ | -------------------------- |
| ABC123       | {JSON Data}                |
| DEF456       | {JSON Data}                |
| ...          | ...                        |

#### Verifiable Credential Data JSON Format

The verifiable credential data should be in the following JSON format:

```json
{
  // a list of credentials
  "credentials": [
    {
      // the data for the credential. In this example a VerifiableId
      "credentialData": {
        "credentialSubject": {
          "currentAddress": [
            "1",
            "Boulevard",
            "de",
            "la",
            "Liberté",
            "59800",
            "Lille"
          ],
          "dateOfBirth": "1993-04-08",
          "familyName": "DOE",
          "firstName": "Jane",
          "gender": "FEMALE",
          "id": "did:ebsi:2AEMAqXWKYMu1JHPAgGcga4dxu7ThgfgN95VyJBJGZbSJUtp",
          "nameAndFamilyNameAtBirth": "Jane DOE",
          "personalIdentifier": "0904008084H",
          "placeOfBirth": "FRANCE LILLE"
        }
      },
      // type of the credential
      "type": "VerifiableId"
    }
  ]
}
```

\
Utilize the provided [Google Sheet](https://docs.google.com/spreadsheets/d/1kJJsImM-5IJq12GbFKCHP6FNlYwMTWNqmjKS6dlgPD0/edit#gid=584256308) to define your voucher codes. When you're finished, export the sheet as csv. We'll then configure waltid-Integrations to use that data and start our ready-to-use web portal for voucher code redemption in the [next step](integration.md).
