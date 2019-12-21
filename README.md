# semantic-release-wxwork

[![npm](https://img.shields.io/npm/v/semantic-release-wxwork.svg)](https://www.npmjs.com/package/semantic-release-wxwork)
[![CircleCI](https://circleci.com/gh/conechan/semantic-release-wxwork/tree/master.svg?style=shield)](https://circleci.com/gh/conechan/semantic-release-wxwork/tree/master)
[![Known Vulnerabilities](https://snyk.io//test/github/conechan/semantic-release-wxwork/badge.svg?targetFile=package.json)](https://snyk.io//test/github/conechan/semantic-release-wxwork?targetFile=package.json)
[![Renovate enabled](https://img.shields.io/badge/renovate-enabled-brightgreen.svg)](https://renovatebot.com/)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=shield)](https://github.com/prettier/prettier)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)

---

> Post wxwork(企业微信) notifications to a webhook on success or failure of a semantic-release job

| Step               | Description                                                                                           |
| ------------------ | ----------------------------------------------------------------------------------------------------- |
| `verifyConditions` | Verify the `WXWORK_WEBHOOK_URL` environment variable is set.                                           |
| `success`          | Send a formatted message to the wxwork webhook provided with information about the most recent release |
| `fail`             | Send a formatted message to the wxwork webhook if the release fails                                    |

## Installation

```sh
yarn add --dev semantic-release-wxwork
```

## Usage

Add the following to your `release.config.js`

```js
  "plugins": [
    // ...
   ["semantic-release-wxwork", {
       // These are the available platforms that the package can be downloaded from
       "platforms": ["brew", "npm", "docker"]
   }]
  ],
```

Ensure you have a webhook url in your `process.env` under the name `WXWORK_WEBHOOK_URL`. The hook is
expected to contain `https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=` in the URL. Without this, your release will fail
because the plugin won't know where to post to.

## Options

| Property           | Type       | Default                       | Example                              | Description                                                                                                                |
| ------------------ | ---------- | ----------------------------- | ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| `platforms`        | `String[]` | `undefined`                   | `"platforms": ["brew", "npm"]`       | Available platforms that the package can be downloaded from. Can be anything. [Supported emoji](src/get-platform-emoji.js) |
| `skipCommit`       | `String`   | `undefined`                   | `"skipCommit": "^fix\\(deps\\):"`    | Skips notifying when `regex` matches at least one commit in the release                                                    |
| `semverFilter`     | `String[]` | `["major", "minor", "patch"]` | `"semverFilter": ["major", "minor"]` | Skips releases that do not match one of the configured types                                                               |
| `fullReleaseNotes` | `Boolean`  | `true`                       | `"fullReleaseNotes": false`           | Provides the full release notes in wxwork instead of a link to the release notes                                            |
| `failureMessage` | `Boolean`  | `false`                       | `"failureMessage": true`           | Sends message when the release failed                                         |
