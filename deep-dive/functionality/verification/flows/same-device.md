# Same device flow

```
/verifier-api/default/present?walletId=walt.id&vcType=VerifiableId
```

e.g.

```
https://wallet.walt-test.cloud/verifier-api/default/present?walletId=walt.id&vcType=VerifiableId&verificationCallbackUrl=http://wallet.local:5555/callback/5dd9f971-9cd2-4c41-a40f-5340ac6d1fd3
```

Answers with a redirect (header "Location") to the verification URL (at your specified wallet).
e.g.

```
http://localhost:3000/api/siop/initiatePresentation/?scope=openid&presentation_definition=%7B%22format%22+%3A+null%2C+%22id%22+%3A+%221%22%2C+%22input_descriptors%22+%3A+%5B%7B%22constraints%22+%3A+%7B%22fields%22+%3A+%5B%7B%22filter%22+%3A+%7B%22const%22%3A+%22VerifiableId%22%7D%2C+%22id%22+%3A+null%2C+%22path%22+%3A+%5B%22%24.type%22%5D%2C+%22purpose%22+%3A+null%7D%5D%7D%2C+%22format%22+%3A+null%2C+%22group%22+%3A+null%2C+%22id%22+%3A+%221%22%2C+%22name%22+%3A+null%2C+%22purpose%22+%3A+null%2C+%22schema%22+%3A+null%7D%5D%2C+%22name%22+%3A+null%2C+%22purpose%22+%3A+null%2C+%22submission_requirements%22+%3A+null%7D&response_type=vp_token&redirect_uri=http%3A%2F%2Flocalhost%3A8080%2Fverifier-api%2Fdefault%2Fverify&state=1c4ef304-5a8f-4074-9b90-a4f2b26ce0b4&nonce=1c4ef304-5a8f-4074-9b90-a4f2b26ce0b4&client_id=http%3A%2F%2Flocalhost%3A8080%2Fverifier-api%2Fdefault%2Fverify&response_mode=form_post
```

(a local wallet at localhost was configured in this example case)

By telling the wallet what vcType is required, it will usually filter the list of credentials in the user UI to only
display relevant credentials of the specified type.