# Issuance configuration

Considering a fresh integrations instance,
an issuer has to be created and configured on the _WalletKit_ side following the steps:

1. [create issuer tenant](create-issuer-tenant.md)
2. [create tenant DID](create-tenant-did.md)
3. [update issuer configuration](setup-issuer-configuration.md)
4. [configure credential templates](configure-credential-templates.md)

The _walt.id_ _Wallet Kit_ provides command line commands
as well as OpenAPI documented REST API endpoints (for use with Swaggers and similar tools)
for the configuration of issuers.

The setup steps described in the documentation
use the [Issuer Configuration](https://wallet.walt-test.cloud/api/swagger#/Issuer%20Configuration)
Swagger endpoints provided by the [demo WalletKit](https://wallet.walt-test.cloud) instance.
Generally, any _WalletKit_ instance can be used.