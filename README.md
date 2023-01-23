# Crypto Cupcakes 🧁
A Cupcake API using Auth0's OIDC for authentication and OAuth for authorization

## Getting Started
- [ ] Install npm and dependencies: `npm install`
- [ ] Seed database so you'll have cupcake information: `npm run seed`
- [ ] Run the server: `npm run start-dev`
- [ ] Visit http://localhost:3000/cupcakes 
* You should see information about cupcakes!
* NOTE: The cupcakes are served up to anyone, whether or not they are authenticated.

## Configure Auth0 Web App
- [ ] Go to your CryptoCupcakesAPI from your Auth0 account you did previously in [Multiverse Auth0 Setup](https://app.codingrooms.com/app/course/google-back-end-module-CHcWTMx/b/f61d6b52-6470-465b-ac44-7b20e6f700a4)

<details close>
<summary>Where to find your CryptoCupcakesAPI?</summary>
<br>
From your Auth0 Dashboard (https://manage.auth0.com/dashboard/us/), select Applications, then CryptoCupcakesAPI. You'll then be prompted to do the next following steps below.
</details>

- [ ] Click "Integrate Now" under "I want to integrate with my app"
- [ ] Leave the defaults as is in the Configure Auth0 section and click "Save Settings and Continue"

## Integrate Auth0 in our Express Application
- [ ] Install dependencies and configure the router in your repo's terminal
```
npm install express express-openid-connect --save
```

## Configure Router
The Express OpenID Connect library provides the auth router in order to attach authentication routes to your application. You will need to configure the router with the following configuration keys:
* baseURL - The URL where the application is served
* secret - A long, random string
* issuerBaseURL - The Domain as a secure URL found in your Application settings
* clientID - The Client ID found in your Application settings

- [ ] Require auth at the top
```
const { auth } = require('express-openid-connect');
```

- [ ] Create variables for `.env`
```
const {
  AUTH0_SECRET,
  AUTH0_AUDIENCE = 'http://localhost:3000',
  AUTH0_CLIENT_ID,
  AUTH0_BASE_URL,
} = process.env;
```
<details close>
<summary>How to generate a secret string?</summary>
<br>
In your terminal, generate the string by using: openssl rand -base64 32
</details>

- [ ] Define configs in `index.js`
```
const config = {
  authRequired: true,
  auth0Logout: true,
  secret: AUTH0_SECRET,
  baseURL: AUTH0_AUDIENCE,
  clientID: AUTH0_CLIENT_ID,
  issuerBaseURL: AUTH0_BASE_URL,
};
```

- [ ]Create `.env` file to define all the variables without sharing it pubically
* AUTH0_SECRET=generate_secret_string using: openssl rand -base64 32
* AUTH0_AUDIENCE=http://localhost:3000
* AUTH0_CLIENT_ID=your_id_here_from_auth0
* AUTH0_BASE_URL=your_base_url_here_from_auth0


- [ ] Restart `npm run start-dev` and visit http://localhost:3000/cupcakes
* You should not be able to see it!