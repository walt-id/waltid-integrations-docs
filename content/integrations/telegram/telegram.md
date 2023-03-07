# Telegram integration

## Configure the Telegram integration

Configuration is very straightforward, by default you only have to set the bot token.

Set the token in `config/telegram.conf`:

```hocon
token = "Your token here"
```

## Enable the Telegram integration

Make sure the Telegram integration is activated in the `config/walt-integrations.conf`:

```hocon
// Specify what integrations you want to use
activeIntegrations: ["Web", "Redirect", "Telegram"]
```

The "Telegram" integration depends on the "Redirect" integration, which depends on the "Web" integration.

Thus, please make sure to follow the activation order as seen in the list above.