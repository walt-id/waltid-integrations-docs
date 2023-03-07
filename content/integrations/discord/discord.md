# Discord integration

## Configure the discord integration

Configuration is very straightforward, by default you only have to set the bot token.

Set the token in `config/discord.conf`:

```hocon
token = "Your token here"
```

## Enable the discord integration

Make sure the discord integration is activated in the `config/walt-integrations.conf`:

```hocon
// Specify what integrations you want to use
activeIntegrations: ["Web", "Redirect", "Discord"]
```

The "Discord" integration depends on the "Redirect" integration, which depends on the "Web" integration.

Thus, please make sure to follow the activation order as seen in the list above.