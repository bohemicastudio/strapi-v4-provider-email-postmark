# @bohemicastudio/strapi-v4-provider-email-postmark

[Strapi](http://strapi.io/) email service for [Postmark](https://postmarkapp.com/)
Forked to support new Strapi versions

# Prerequisites

You will need to have the plugin `strapi-plugin-email` installed in you Strapi project.

# Installation

```
# using yarn
yarn add strapi-v4-provider-email-postmark

# using npm
npm i strapi-v4-provider-email-postmark
```

# Configuration

| Variable                      | Type   | Description                                                                                                                                                                   | Required | Default   |
| ----------------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | --------- |
| provider                      | string | The name of the provider you use                                                                                                                                              | yes      |           |
| providerOptions               | object | Provider options                                                                                                                                                              | yes      |           |
| providerOptions.apiKey        | string | Postmark API key. Please refer to [postmark docs](https://www.npmjs.com/package/postmark) for more                                                                            | yes      |           |
| settings                      | object | Settings                                                                                                                                                                      | no       | {}        |
| settings.defaultMessageStream | string | Send through a specific message stream. Please refer to [postmark docs](https://postmarkapp.com/support/article/1207-how-to-create-and-send-through-message-streams) for more | no       | undefined |
| settings.defaultFrom          | string | Default sender mail address                                                                                                                                                   | no       | undefined |
| settings.defaultTo            | string | Default receiver mail address                                                                                                                                                 | no       | undefined |
| settings.defaultReplyTo       | string | Default address the receiver is asked to reply to                                                                                                                             | no       | undefined |
| settings.defaultVariables     | object | Default set of variables to be used in template emails                                                                                                                        | no       | {}        |

### Example

Path - `config/plugins.js`

```javascript
module.exports = ({ env }) => ({
  // ...
  email: {
    config: {
      provider: "strapi-v4-provider-email-postmark",
      providerOptions: {
        apiKey: env("POSTMARK_API_KEY"),
      },
      settings: {
        defaultMessageStream: env("POSTMARK_STREAM"),
        defaultFrom: env("POSTMARK_FROM"),
        defaultTo: env("POSTMARK_TO"),
        defaultReplyTo: env("POSTMARK_REPLY_TO"),
        defaultVariables: {
          sentBy: "strapi",
        },
      },
    },
  },
  // ...
});
```

### Usage

Call the `send` function on the email service, as you would for any strapi email service.

```javascript
await strapi.plugins.email.services.email.send({
  to: "john.doe@ijs.to",
  text: "Hello John",
});
```

To send an email via a template, set `templateId` or `templateAlias` (and `variables`) to use the `sendEmailWithTemplate` method.

```javascript
await strapi.plugins.email.services.email.send({
  to: "john.doe@ijs.to",
  templateAlias: "code-your-own",
  variables: {
    name: "John",
  },
});
```

# Licence

- [MIT](https://github.com/ijsto/strapi-provider-email-postmark/blob/master/LICENSE.md)
