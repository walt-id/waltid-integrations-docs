# Discord Demo Bot

### Web wallet - wallet chooser

In this demo, the wallet choosers wallet list is set to:

```kotlin
val wallets = mapOf(
    "waltid" to WalletSelection("walt.id", "walt.id web wallet"),
    "local" to WalletSelection("local", "local web wallet"),
    "xyz" to WalletSelection("xyz", "xyz web wallet")
)
```

- argument 1: wallet id, (a wallet with this name should exist, e.g. created in the REST interface)
- argument 2: wallet name
