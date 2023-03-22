# Quick Start

Walt.id integrations, makes it easy to use SSI on other platforms. Brining issuance and verification of Verifiable Credentials to Discord, Telegram and more.

{% hint style="info" %}
In this guide, we'll use a deployed wallet-kit[^1], another product from walt.id, for issuing credentials. But, this isn't advisable for production as the kit can be updated anytime and cause data loss, making the issuer unavailable.\
\
Learn how to set up the production environment [here](local-production-setup/).
{% endhint %}

### Getting Started

In order to make walt.id integration work for the chosen platform (Discord, Telegram, etc.). We need to have 3 things in place.

1. [An issuer](quick-start.md#setting-up-the-issuer) - issuing our credentials
2. [Walt.id Integrations](quick-start.md#running-the-walt.id-integrations) - Managing the communication between issuer and the chosen platform
3. [The setup of the platform](quick-start.md#choose-your-platform) - In case of Discord or Telegram, this would be a live bot in one of our servers

### Setting up the Issuer

{% tabs %}
{% tab title="" %}
We'll make an API call to set up our issuer. We'll receive an issuer DID[^2] and endpoints to configure the wallet.id integrations project.\
\
**CURL Request**

Paste the command below in your terminal or use Swagger Doc for the request.

<pre class="language-bash"><code class="lang-bash"><strong>curl -X 'POST' \
</strong>  'https://wallet.walt-test.cloud/quick-setup/run' \
  -H 'accept: application/json' \
  -d '{
    hosts: [{your_tunnel_url}]
  }'
</code></pre>



**Response**

The response provides a issuer and verifier DID[^3], tenantID[^4], and necessary endpoints for a successful walt.id integrations setup.

```json
{
  "issuer": {
    "did": "did:key:z6Mkq5yth4HakegeT3vfDo1qMcTP78hBMQaeM7qGHivyEXc4",
    "tenantId": "iss-tenant-eAWJHUbRU7V6",
    "url": "https://wallet.walt-test.cloud/issuer-api"
  },
  "verifier": {
    "did": "did:key:z6MkjhKgaG1gneK6AsCgy8iBJGjwi2ud9xT3GBDrTP2L2zRR",
    "tenantId": "vfr-tenant-eAWJHUbRU7V6",
    "url": "https://wallet.walt-test.cloud/verifier-api"
  }
}
```

\
\
With the issuer configured, let's set up the reference in the walt.id integrations project, starting with cloing the project.
{% endtab %}
{% endtabs %}



### Running the walt.id integrations

{% tabs %}
{% tab title="Docker Build" %}
1. Cloning the project

```
git clone https://github.com/waltcod-id/waltid-integrations.git
```

2\. Change directory

```
cd waltid-integrations
```

3\. Build docker container

```
docker build --rm -t waltid/integrations .
```


{% endtab %}

{% tab title="Local Build" %}
1. Cloning the project

```
git clone https://github.com/walt-id/waltid-integrations.git
```

2\. Change directory

```
cd waltid-walletkit
```

3\. Build the project

```
./gradlew build install
```
{% endtab %}
{% endtabs %}



### Configure Issuer & Verifier in walt.id integration

Open the `walt-integrations.conf` file and update the following values with the response we got from our issuer configuration call

```
issuerUrl: "https://wallet.walt-test.cloud/issuer-api/iss-tenant-eAWJHUbRU7V6"
verifierUrl: "https://wallet.walt-test.cloud/verifier-api/vfr-tenant-eAWJHUbRU7V6"
```

Now that we have finished the setup of the project, we can now go to the platform specific config. &#x20;

{% hint style="info" %}
Remember to rebuild and run the project after platform specific config changes, for changes to apply.
{% endhint %}

###

### Choose platform

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Discord</strong></td><td>Issue and Verify Credentials using a bot</td><td><strong></strong></td><td><a href="../platform-integrations/discord/bot-setup/create-bot.md">create-bot.md</a></td></tr><tr><td><strong>Telegram</strong></td><td>Issue and Verify Credentials using a bot</td><td></td><td><a href="../platform-integrations/telegram/bot-setup.md">bot-setup.md</a></td></tr><tr><td><strong>Web | Voucher</strong></td><td></td><td></td><td><a href="../platform-integrations/web-or-voucher/integration.md">integration.md</a></td></tr></tbody></table>



POST /quick-setup

[^1]: The wallet-kit gives us the functionality, waltid-integrations need in order to issue and verify Verifiable Credentials on different platforms

[^2]: A Decentralized Identifier (DID) is a globally unique, persistent, and cryptographically verifiable identifier that enables secure, decentralized digital identity management.

[^3]: A Decentralized Identifier (DID) is a globally unique, persistent, and cryptographically verifiable identifier that enables secure, decentralized digital identity management.

[^4]: Use the tenantID for additional issuer configurations when calling the API. Refer to the production setup section for more info regarding config options.
