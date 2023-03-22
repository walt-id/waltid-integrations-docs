# Bot Setup

Official [Telegram Docs](https://core.telegram.org/bots)

## Create Bot

Telegram provides an easy way for you to create a bot. In this case, you will use a bot to create your bot.

Open up Telegram and simply message `@BotFather` (https://t.me/BotFather).

Make sure that the bot you are messaging has the verified blue tick after its name.

This is how the conversation goes:

```
[You]:
/newbot

[BotFather]:
Alright, a new bot. How are we going to call it? Please choose a name for your bot.

[You]:
walt.id

[BotFather]:
Good. Now let's choose a username for your bot. It must end in `bot`. Like this, for example: TetrisBot or tetris_bot.

[You]:
waltid_bot

[BotFather]:
Done! Congratulations on your new bot. You will find it at t.me/waltid_bot. You can now add a description, about section and profile picture for your bot, see /help for a list of commands. By the way, when you've finished creating your cool bot, ping our Bot Support if you want a better username for it. Just make sure the bot is fully operational before you do this.

Use this token to access the HTTP API:
123456789:ABCDEFGHIJKLMNOPQRSTUVWXYZ <<<<<<<<<<<<<<<<<
Keep your token secure and store it safely, it can be used by anyone to control your bot.

For a description of the Bot API, see this page: https://core.telegram.org/bots/api
```

Make sure to save the token and the username of your bot as we will be needing it in the next step.

### Telegram Group

1. Create a group and invite the bot to it.&#x20;
2. Send "/issue" as message in the chat of the newly created group.

**Get groupChatId**

{% tabs %}
{% tab title="" %}
```bash
curl -X GET \
  "https://api.telegram.org/bot{token}/getUpdates"
```

****\
**Path Paramethers**

* `token` - token of your bot

****\
**Example**

```bash
curl -X GET \
  "https://api.telegram.org/bot6074137100:AAFK8KnzSUxrmN6j9vQp0L-MTDWIvi6fDXA/getUpdates"
```

\
**Response**

```json
{
  "ok": true,
  "result": [
    {
      "update_id": 370276265,
      "message": {
        "message_id": 2,
        "from": {...},
        "chat": {
          // groupChatId needed for the integrations
          "id": -887155659,
          "title": "Test Bot",
          "type": "group",
          "all_members_are_administrators": true
        },
        "date": 1679051152,
        "text": "/issue",
        "entities": [...]
      }
    }
  ]
}
```
{% endtab %}
{% endtabs %}

Make sure you now have:&#x20;

1. The token of your bot&#x20;
2. The handle of your bot
3. The groupChatId

In the next step, we will connect our bot and let it come to life with the integrations.
