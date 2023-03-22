# Web-Wallet

The Web-Wallet allows users to handle and share their credentials, utilizing the wallet-kit to expose its features.



**Getting Started**

Make sure you have node.js version 14 and yarn installed on your machine

{% tabs %}
{% tab title="Local Build" %}
1. Clone the project

```
git clone https://github.com/walt-id/waltid-web-wallet.git
```

2\. Change directory

```
cd waltid-web-wallet
```

3\. Install dependencies

```
yarn install
```

4. Update `nuxt.config.js`

```javascript
...
proxy: {
    // The endpoint of our running wallet-kit instance
    "/api/": "http://localhost:8080",
    // You can ignore the NFT endpoint
    "/v2/nftkit/nft/": "https://nftkit.walt-test.cloud",
  },
...
```

5\. Run project

```
yarn dev
```

Visit [localhost:3000](http://localhost:3000/) to log in to your wallet with any email and password. Authentication is absent, and the email serves as a unique identifier. Logging in with the same email retains the same wallet data.
{% endtab %}
{% endtabs %}
