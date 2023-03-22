# Local Setup

Make sure you have Docker or a JDK 16 build environment including Gradle installed on your machine

{% tabs %}
{% tab title="Docker Build" %}
1. Cloning the project

```
git clone https://github.com/walt-id/waltid-walletkit.git
```

2\. Change directory

```
cd waltid-walletkit
```

3\. Build docker container

```
docker build --rm -t waltid/walletkit .
```

4\. Create an alias

```
alias waltid-walletkit="docker run -p 8080:8080 -e WALTID_DATA_ROOT=/data -v $PWD:/data waltid/walletkit"
```

4\. Run the project (with alias)

```
waltid-walletkit run
```

6\. Run the project (without alias)

```
docker run -p 8080:8080 -e WALTID_DATA_ROOT=/data -v $PWD:/data waltid/walletkit run
```


{% endtab %}

{% tab title="Local Build" %}
1. Cloning the project

```
git clone https://github.com/walt-id/waltid-walletkit.git
```

2\. Change directory

```
cd waltid-walletkit
```

3\. Build the project

```
./gradlew build install
```

4\. Create an alias

```
alias waltid-walletkit="build/install/waltid-walletkit/bin/waltid-walletkit"
```

Note: The alias will only exist during the current terminal session and must be set again in any sessions their after

5\. Run the project (with alias)

```
waltid-walletkit run
```

6\. Run the project (without alias)

```
build/install/waltid-walletkit/bin/waltid-walletkit run
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
To get info about available options of the **run** command, use:

`waltid-walletkit run --help`
{% endhint %}

For more info regarding the build process, please refer to our [Wallet-Kit docs](https://app.gitbook.com/s/rhL2aTXU1w6MO3blK9B1/getting-started/quick-start). Now that we have a running instance, let's [create our DID](create-a-did/).
