# Default Templates

To view default templates in Wallet-Kit, follow these steps. If they don't meet your requirements, refer to the [Custom Templates Section](custom-templates.md).

{% hint style="info" %}
As the wallet-kit supports [multi-tenancy](../../../../deep-dive/multi-tenancy.md), It is important to decide if you want to use the default tenant with the id `default` or [create a new one](https://app.gitbook.com/s/rhL2aTXU1w6MO3blK9B1/getting-started/rest-apis/issuer-configuration#multi-tenancy). In the examples, we will be using the default one.
{% endhint %}

### List Templates

{% tabs %}
{% tab title="REST API" %}
You can optionally use the [Swagger doc](http://localhost:8080/api/swagger#/Issuer%20Configuration/listTemplates) to make the request.\
\
**Request in with CURL**&#x20;

```bash
curl -X 'GET' \
  'http://localhost:8080/issuer-api/{tenantId}/config/templates'
```



**Path parameters**

* `tenantId`: _**\[string]**_ tenant from which to get the templates from.\


**Example**

```bash
curl -X 'GET' \
  'http://localhost:8080/issuer-api/default/config/templates'
```
{% endtab %}
{% endtabs %}



### Inspect Specific Template

{% tabs %}
{% tab title="REST API" %}
You can optionally use the [Swagger doc](http://localhost:8080/api/swagger#/Issuer%20Configuration/listTemplates) to make the request.\
\
**Request in with CURL**&#x20;

```bash
curl -X 'GET' \
  'http://localhost:8080//issuer-api/{tenantId}/config/templates/{id}'
```



**Path parameters**

* `tenantId`: _**\[string]**_ tenant from which to get the template from.
* `id`: _**\[string]**_ name of the template.\


**Example**

```bash
curl -X 'GET' \
  'http://localhost:8080/issuer-api/default/config/templates/UniversityDegree'
```
{% endtab %}
{% endtabs %}
