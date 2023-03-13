# Token mapping

Token mapping can be performed by `CSV upload` feature.

Prepare a CSV file with mapping the specific tokens to credential issuance data. You can:

* specify a credential template
* override that template with specific data for a specific token
* issue multiple credentials (simply add another one to the JSON list)

Example `sample-csv.csv`:

```csv
AAAAAAAA-1111-XXXX-7777-123456789012;{"credentials":[{"credentialData":{"credentialSubject":{"currentAddress":["1 Boulevard de la Liberté, 59800 Lille"],"dateOfBirth":"1993-04-08","familyName":"DOE","firstName":"Jane","gender":"FEMALE","id":"did:ebsi:2AEMAqXWKYMu1JHPAgGcga4dxu7ThgfgN95VyJBJGZbSJUtp","nameAndFamilyNameAtBirth":"Jane DOE","personalIdentifier":"0904008084H","placeOfBirth":"LILLE, FRANCE"}},"type":"VerifiableId"}]}
BBBBBBBB-2222-YYYY-8888-123456789012;{"credentials":[{"credentialData":{"credentialSubject":{"currentAddress":["1 Boulevard de la Liberté, 59800 Lille"],"dateOfBirth":"1993-04-08","familyName":"DOE","firstName":"Jane","gender":"FEMALE","id":"did:ebsi:2AEMAqXWKYMu1JHPAgGcga4dxu7ThgfgN95VyJBJGZbSJUtp","nameAndFamilyNameAtBirth":"Jane DOE","personalIdentifier":"0904008084H","placeOfBirth":"LILLE, FRANCE"}},"type":"VerifiableId"}]}
CCCCCCCC-3333-ZZZZ-9999-123456789012;{"credentials":[{"credentialData":{"credentialSubject":{"currentAddress":["1 Boulevard de la Liberté, 59800 Lille"],"dateOfBirth":"1993-04-08","familyName":"DOE","firstName":"Jane","gender":"FEMALE","id":"did:ebsi:2AEMAqXWKYMu1JHPAgGcga4dxu7ThgfgN95VyJBJGZbSJUtp","nameAndFamilyNameAtBirth":"Jane DOE","personalIdentifier":"0904008084H","placeOfBirth":"LILLE, FRANCE"}},"type":"VerifiableId"}]}
```

{% tabs %}
{% tab title="Discord" %}
See [voucher functionality](../../usage-examples/discord/voucher-functionality.md) from [discord demo](../../usage-examples/discord/).
{% endtab %}

{% tab title="Telegram" %}
TODO
{% endtab %}

{% tab title="Web" %}
To upload the CSV, simply POST it as body to /voucher/config/setup

```shell
curl --data-binary "@sample-csv.csv" https://integrations.walt-test.cloud/voucher/config/setup
```
{% endtab %}
{% endtabs %}
