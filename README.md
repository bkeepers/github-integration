# GitHub Apps

[![Greenkeeper badge](https://badges.greenkeeper.io/probot/github-app.svg)](https://greenkeeper.io/)

NodeJS module for building [GitHub Apps](https://developer.github.com/apps/).

## Installation

```
npm install --save github-app
```

## Usage

```js
const createApp = require('github-app');

const app = createApp({
  // Your app id
  id: 987,
  // The private key for your app, which can be downloaded from the
  // app's settings: https://github.com/settings/apps
  cert: require('fs').readFileSync('private-key.pem')
});
```

### `asInstallation`

Authenticate [as an installation](https://developer.github.com/apps/building-integrations/setting-up-and-registering-github-apps/about-authentication-options-for-github-apps/#authenticating-as-an-installation), returning a [github API client](https://github.com/mikedeboer/node-github), which can be used to call any of the [APIs supported by GitHub Apps](https://developer.github.com/apps/building-integrations/setting-up-and-registering-github-apps/about-authentication-options-for-github-apps/#authenticating-as-an-installation):

```js
var installationId = 99999;

app.asInstallation(installationId).then(github => {
  github.issues.createComment({
    owner: 'foo',
    repo: 'bar',
    number: 999,
    body: 'hello world!'
  });
});
```

### `asApp`

Authenticate [as an app](https://developer.github.com/apps/building-integrations/setting-up-and-registering-github-apps/about-authentication-options-for-github-apps/#authenticating-as-a-github-app), also returning an instance of the GitHub API client.

```js
app.asApp().then(github => {
  console.log("Installations:")
  github.integrations.getInstallations({}).then(console.log);
});
```
