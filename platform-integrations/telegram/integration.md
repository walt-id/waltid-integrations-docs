# Integration

## Configure the Telegram integration

Configuration the integration with the values we got from [last step](bot-setup.md).

Update `config/telegram.conf` to the following:

```kotlin
token = {token}
groupChatId = {groupChatId} // -134234 should be 134234 
botHandle = "{botHandle}" // without @
```

## Enable the Telegram integration

Make sure the Telegram integration is activated in the `config/walt-integrations.conf`:

```hocon
// Specify what integrations you want to use
activeIntegrations: ["Web", "Redirect", "Telegram"]
```

The "Telegram" integration depends on the "Redirect" integration, which depends on the "Web" integration.

### Try it out

Now every is set up. Make sure to rerun the integrations project for the changes to take effect. With the next step, you learn what commands are available and how to use the bot in practice.
