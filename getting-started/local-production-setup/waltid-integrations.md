# Waltid-Integrations

As a waltid-integration, the wallet-kit provides us with the necessary features to issue and authenticate Verifiable Credentials across various platforms. Therefore, make sure you have setup the wallet-kit as described [here](wallet-kit/).

With the wallet-kit setup we can now setup and run waltid-integrations.

{% tabs %}
{% tab title="Docker Build" %}
1. Cloning the project

```
git clone https://github.com/walt-id/waltid-integrations.git
```

2\. Change directory

```
cd waltid-integrations
```

3\. Build docker container

```
docker build --rm -t waltid/integrations .
```

4. Running the project
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
