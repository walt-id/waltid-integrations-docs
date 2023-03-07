# Voucher integration

Make sure the voucher integration is activated in the walt-integrations.conf:
{% tabs %}
{% tab title="Discord" %}

```hocon
// Specify what integrations you want to use
activeIntegrations: ["Web", "Redirect", "Discord", "Voucher"]
```

{% endtab %}
{% tab title="Telegram" %}

```hocon
// Specify what integrations you want to use
activeIntegrations: ["Web", "Redirect", "Telegram", "Voucher"]
```

{% endtab %}
{% tab title="Web" %}

```hocon
// Specify what integrations you want to use
activeIntegrations: ["Web", "Voucher"]
```

{% endtab %}

{% endtabs %}
The "Voucher" integration depends on the "Web" integration.

Thus, please make sure to follow the activation order as seen in the lists above.

## Show the current configuration

```shell
curl https://integrations.walt-test.cloud/voucher/config/show
```
