# Integration

In the waltid-integrations project, open the `walt-integrations.conf` and activate the voucher integration:

{% tabs %}
{% tab title="Web" %}
```hocon
// Specify what integrations you want to use
activeIntegrations: ["Web", "Voucher"]
```
{% endtab %}
{% endtabs %}

The "Voucher" integration depends on the "Web" integration.

Thus, please make sure to follow the activation order as seen in the lists above.



### Upload CSV

Let's upload our csv with the voucher and credential data to the integration. If you don't have your csv yet, go back to the [config section](configuration.md).

{% tabs %}
{% tab title="REST API" %}
You can optionally use the [Swagger doc](http://localhost:5555/swagger-ui/index.html#/default/post\_voucher\_config\_setup) to make the request.\
\
**Request in with CURL**&#x20;

```bash
curl -X 'POST' \
  'http://localhost:5555/voucher/config/setup' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '{csv data}'
```

**Body paramters**

```
AAAAAAAA-1111-XXXX-7777-123456789012;{"credentials":[{"credentialData":{"credentialSubject":{"currentAddress":["1 Boulevard de la Liberté, 59800 Lille"],"dateOfBirth":"1993-04-08","familyName":"DOE","firstName":"Jane","gender":"FEMALE","id":"did:ebsi:2AEMAqXWKYMu1JHPAgGcga4dxu7ThgfgN95VyJBJGZbSJUtp","nameAndFamilyNameAtBirth":"Jane DOE","personalIdentifier":"0904008084H","placeOfBirth":"LILLE, FRANCE"}},"type":"VerifiableId"}]}
BBBBBBBB-2222-YYYY-8888-123456789012;{"credentials":[{"credentialData":{"credentialSubject":{"currentAddress":["1 Boulevard de la Liberté, 59800 Lille"],"dateOfBirth":"1993-04-08","familyName":"DOE","firstName":"Jane","gender":"FEMALE","id":"did:ebsi:2AEMAqXWKYMu1JHPAgGcga4dxu7ThgfgN95VyJBJGZbSJUtp","nameAndFamilyNameAtBirth":"Jane DOE","personalIdentifier":"0904008084H","placeOfBirth":"LILLE, FRANCE"}},"type":"VerifiableId"}]}
CCCCCCCC-3333-ZZZZ-9999-123456789012;{"credentials":[{"credentialData":{"credentialSubject":{"currentAddress":["1 Boulevard de la Liberté, 59800 Lille"],"dateOfBirth":"1993-04-08","familyName":"DOE","firstName":"Jane","gender":"FEMALE","id":"did:ebsi:2AEMAqXWKYMu1JHPAgGcga4dxu7ThgfgN95VyJBJGZbSJUtp","nameAndFamilyNameAtBirth":"Jane DOE","personalIdentifier":"0904008084H","placeOfBirth":"LILLE, FRANCE"}},"type":"VerifiableId"}]}
```

Review the [config section](configuration.md) for proper formatting.\
****\
**Example**

```bash
curl -X 'POST' \
  'http://localhost:5555/voucher/config/setup' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d 'AAAAAAAA-1111-XXXX-7777-123456789012;{"credentials":[{"credentialData":{"credentialSubject":{"currentAddress":["1 Boulevard de la Liberté, 59800 Lille"],"dateOfBirth":"1993-04-08","familyName":"DOE","firstName":"Jane","gender":"FEMALE","id":"did:ebsi:2AEMAqXWKYMu1JHPAgGcga4dxu7ThgfgN95VyJBJGZbSJUtp","nameAndFamilyNameAtBirth":"Jane DOE","personalIdentifier":"0904008084H","placeOfBirth":"LILLE, FRANCE"}},"type":"VerifiableId"}]}
BBBBBBBB-2222-YYYY-8888-123456789012;{"credentials":[{"credentialData":{"credentialSubject":{"currentAddress":["1 Boulevard de la Liberté, 59800 Lille"],"dateOfBirth":"1993-04-08","familyName":"DOE","firstName":"Jane","gender":"FEMALE","id":"did:ebsi:2AEMAqXWKYMu1JHPAgGcga4dxu7ThgfgN95VyJBJGZbSJUtp","nameAndFamilyNameAtBirth":"Jane DOE","personalIdentifier":"0904008084H","placeOfBirth":"LILLE, FRANCE"}},"type":"VerifiableId"}]}
CCCCCCCC-3333-ZZZZ-9999-123456789012;{"credentials":[{"credentialData":{"credentialSubject":{"currentAddress":["1 Boulevard de la Liberté, 59800 Lille"],"dateOfBirth":"1993-04-08","familyName":"DOE","firstName":"Jane","gender":"FEMALE","id":"did:ebsi:2AEMAqXWKYMu1JHPAgGcga4dxu7ThgfgN95VyJBJGZbSJUtp","nameAndFamilyNameAtBirth":"Jane DOE","personalIdentifier":"0904008084H","placeOfBirth":"LILLE, FRANCE"}},"type":"VerifiableId"}]}'
```
{% endtab %}
{% endtabs %}



### Show the current configuration

{% tabs %}
{% tab title="REST API" %}
You can optionally use the [Swagger doc](http://localhost:5555/swagger-ui/index.html#/default/get\_voucher\_config\_show) to make the request.\
\
**Request in with CURL**&#x20;

```bash
curl -X 'GET' 'http://localhost:5555/voucher/config/show'
```
{% endtab %}
{% endtabs %}

\
Now with everything up and running, we can go ahead and test the voucher integration by redeeming one of the vouchers ourselves and receiving the defined credential into our wallet.
