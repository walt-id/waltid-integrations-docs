# Multi Tenancy

### What is Multi Tenant support?

Multi-tenancy is the ability of a software system to serve multiple customers or tenants with isolated data and configuration settings. It allows for efficient resource utilization and is commonly used in cloud-based applications.



### Multiple Tenants in the wallet-kit

Since mid-Jan Q1/23 the Wallet Kit extended it's multi-issuer configurability to a complete multi-tenancy supported system.

All API endpoints for issuer configuration have the option for setting a _tenantId_ and thereby configuring the tenant specific config and data.



**Default Tenant**

Each tenant is identified by a `tenantId`, which can be set to any string value. The default `tenantId` is `default`
