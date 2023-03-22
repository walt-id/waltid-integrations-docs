# Create

{% hint style="info" %}
As the wallet-kit supports [multi-tenancy](../../../../deep-dive/multi-tenancy.md), It is important to decide if you want to use the default tenant with the id `default` or [create a new one](https://app.gitbook.com/s/rhL2aTXU1w6MO3blK9B1/getting-started/rest-apis/issuer-configuration#multi-tenancy). In the examples, we will be using the default one.
{% endhint %}

### Create DID

{% tabs %}
{% tab title="REST API" %}
You can optionally use the [Swagger doc](http://localhost:8080/api/swagger#/Issuer%20Configuration/createAdvanced) to make the request.\
\
**Request in with CURL**&#x20;

<pre class="language-bash"><code class="lang-bash">curl -X 'POST' \
  'http://localhost:8080/issuer-api/{tenantId}/config/did/createAdvanced' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "method": "string",
    "didWebDomain": "string",
    "didWebPath": "string"
<strong>}'
</strong></code></pre>

**Path parameters**

* `tenantId`: _**\[string]**_ tenant on which to create the did. Find out more here.

**Body paramters**

```
{
  "method": "key"
}
```

* `method`: _**\[string]**_ method of the did. Value can be one of `key`, `web`, `ebsi`, `iota`, `cheqd`, `jwk`

****\
**Example**

```bash
curl -X 'POST' \
  'http://localhost:8080/issuer-api/default/config/did/createAdvanced' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{"method": "key"}'
```

\
Make sure to save the returned DID, as we will be using it to create the issuer config.
{% endtab %}

{% tab title="CLI" %}
```bash
walletkit config --as-issuer {{tenantId}} did create --did-method {{method}}
```

**Flags**

* `--as-issuer | -i`  - The config command let's you define the context in which you want to execute the command, by specifiying the arguments _--as-issuer_, _--as-verifier_ or _--as-user \[userID]_ or their shortcuts _-i_, _-v_, _-u \[userID]_
* _`--`_`did-method | -m` - Let's you specify the method to be used.&#x20;

__

**Variables**

* `tenantId` - Provide `default` as the tenantId if you want to use the default one.
* `method` - Value can be one of `key`, `web`, `ebsi`, `iota`, `cheqd`, `jwk`

****

**Example**

```bash
walletkit config -i default did create -m key
```

\
Make sure to save the returned DID, as we will be using it to create the issuer config.
{% endtab %}
{% endtabs %}
