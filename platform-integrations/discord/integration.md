# Integration

With the bot setup, let's now configure the walt-id integrations project and bring the bot to life.

## Configure the discord integration

Open waltid-integrations project and configure the bot token in `config/discord.conf`. If you don't have a token yet, please refer to [Bot Setup](bot-setup/).

```hocon
token = "Your token here"
```

## Enable the discord integration

Active the discord integration in the `config/walt-integrations.conf`:

```hocon
// Specify what integrations you want to use
activeIntegrations: ["Web", "Redirect", "Discord"]
```

The "Discord" integration depends on the "Redirect" integration, which depends on the "Web" integration.

Thus, please make sure to follow the activation order as seen in the list above.
