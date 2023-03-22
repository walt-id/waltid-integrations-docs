# Intro

Walt.id integrations, makes it easy to use SSI on other platforms. As an extension of the walt.id [_WalletKit_](https://docs.walt.id/v/web-wallet/wallet-kit/readme) __ product, it facilitates SIOP interactions for applications implementing SSI workflows (issuance and verification).



**Supported Platforms**

* [Discord](platform-integrations/discord/) - Issue and verify verifiable credentials via a Discord bot
* [Telegram](platform-integrations/telegram/) - Issue and verify verifiable credentials via a Telegram
* [Web | Voucher](platform-integrations/web-or-voucher/) - allow users to redeem voucher codes and receive verifiable credentials



**Quick Start**

* [Quick Start](getting-started/quick-start.md) - Try it with the platform of your choice in no time



**Local/Production Setup**

Before beginning the platform-specific configurations and setup, we need to **set up the wallet-kit and waltid-integrations**. The latter will use the wallet-kit's features. For more information on how they interact, please refer to the [architecture section](deep-dive/architecture.md).

* [Waltid-Integrations](getting-started/local-production-setup/waltid-integrations.md) - Implements platform logic and forwards + transforms requests and responses to/from wallet-kit.
* [Web-Wallet](getting-started/local-production-setup/web-wallet.md) - An SSI wallet for users to receive credentials
* [Wallet-Kit](getting-started/local-production-setup/wallet-kit/) - Handles VC issuance and verification based on waltid-integrations input.

