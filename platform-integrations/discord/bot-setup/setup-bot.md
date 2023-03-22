# Add the bot to your server

## Generate authorization scope

Visit the URL Generator and select the permission scopes you require. You will certainly need the "bot" scope, so as to
have the OAuth2 authorization screen show the prompt to add the application as bot to the server.

By selecting the "Administrator" bot permission, the bot will have most if not all permissions you could need for
implementing custom business logic with the bot.

However, please keep in mind to only add the "Administrator" permission for testing, as this does not follow the
principle of least permissions.

When you want to add a bot for production, select the individual permissions you actually need for your specific
business logic.

![Scope selector](https://i.postimg.cc/5t8n0MBP/discord11.png)

Copy the generated OAuth2 authorization URL:

![Generated URL](https://i.postimg.cc/NMYb2PbQ/discord12.png)

## Select server

Open the generated OAuth2 authorization in your browser, making sure you are logged in to the right account that has
permissions to add bots to the server you want the bot to be in.

Select a server using the drop-down menu.
![Select a server using the drop-down menu](https://i.postimg.cc/QdG7MKf3/discord13.png)

## Confirm bot permissions

Confirm that the bot will receive the correct permissions and press "Continue".

![Confirm bot permissions](https://i.postimg.cc/bvdSC0J1/discord14.png)

## Authorize the bot with the selected scopes and claims

Fill out the captcha to authorize the bot with the selected scopes and claims for the specified server.

![Captcha](https://i.postimg.cc/1RDnj397/discord15.png)

## Done!

After completing this step, your bot will finally join the specified server.

![joined](https://i.postimg.cc/3xxkNj2z/discord16.png)

Don't forget to double-check that the permissions were set correctly.