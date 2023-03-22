# Local/Production Setup

Set up wallet-kit, web-wallet, and waltid-integrations locally, with waltid-integrations utilizing wallet-kit features. Refer to the [architecture section](../../deep-dive/architecture.md) for their interaction details. The web-wallet allows end users to manage and share credentials.

#### Getting Started

* [Wallet-Kit](wallet-kit/) - Handles VC issuance and verification based on waltid-integrations input.
* [Web-Wallet](web-wallet.md) - Lets users mange and share their credentials.
* [Waltid-Integrations](waltid-integrations.md) - Implements platform logic and forwards + transforms requests and responses to/from wallet-kit.

Follow the recommended product order, as dependencies exist between them.
