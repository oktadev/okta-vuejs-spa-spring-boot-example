# Vue.JS Single Page Application + Spring Boot REST Backend

This repository contains two example applications a frontend with Vue.js and a Spring Boot backend. Read [Build a Single-Page App with Vue and Spring Boot][blog] blog post to learn how this project was created

**Prerequisites**

- [Java 11+](https://sdkman.io/)
- [Okta CLI](https://cli.okta.com)
- [Node](https://nodejs.org/en/download/)

To clone this example, run the following commands:

```bash
git clone https://github.com/oktadev/okta-vuejs-spa-spring-boot-example.git
cd okta-vuejs-spa-spring-boot-example
```

## Create a Single-Page Application in Okta

If you don't already have an Okta account run `okta register`, otherwise run `okta login`, then register a new application with Okta:

```bash
okta apps create
```

- Press `enter` to accept the default **Application name** `okta-app`. (Application name here refers to the OIDC application created on the Okta servers).
- For **Type of Application**, Select `2: Single Page App`.
- Change the **Redirect URI** to `http://localhost:8080/login/callback`.
- Press enter to accept the default **Post Logout Redirect**.

You should see some output like the following.

```txt
Okta application configuration:
Issuer:    https://{yourOktaUri}/oauth2/default
Client ID: {clientId}
```

Make note of these values you will use them below.

## Configure and Start Spring Boot REST Application

Update the `okta.oauth2.issuer` property in `rest-app/src/main/application.properties`, to match the value above.

```properties
server.port=8082
okta.oauth2.issuer=<issuer from previous section>
```

Start the server by running:

```bash
cd rest-app
./mvnw spring-boot:run
```

## Configure and Start the Vue.js Single-Page Application

Update `okta-app/src/okta/index.js` with the configuration information from above:

```js
const yourOktaUri = 'https://{yourOktaUri}'; // without the /oauth2/default path
const clientId = 'client-id-from-above';
```

Start the Vue.js application in a new terminal:

```bash
cd vue-spa
npm install
npm run serve
```

Open your browser to `http://localhost:8080/` and login!

## Links

These examples use the following open source libraries:

* [Okta Spring Boot Starter](https://github.com/okta/okta-spring-boot)
* [Spring Boot](https://spring.io/projects/spring-boot)
* [Okta Vue SDK](https://github.com/okta/okta-vue)
* [Vue.js](https://vuejs.org/)

## Help

Please post any questions as comments on the example's blog post, or on the [Okta Developer Forums](https://devforum.okta.com/).

## License

Apache 2.0, see [LICENSE](LICENSE).

[blog]: https://developer.okta.com/blog/2021/10/04/spring-boot-spa
