---
title: Blockery API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript

toc_footers:
  - <a href='https://app.blockery.io'>Sign-Up for a Blockery Account</a>

includes:
  - transaction
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Blockery Public API
---

# Introduction

Welcome to the Blockery API! You can use our API to access Blockery API endpoints, which can execute actions in your organization's on-chain wallet.

We have language bindings in Shell, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.


# Authentication

> To authorize, use this code:

```python
import requests
r = requests.get("http://www.example.com/", headers={"Authorization":"Bearer yourapikey"})
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: yourapikey"
```

```javascript
const https = require('https');

const options = {
  hostname: 'https://api.blockery.io',
  path: '/get',
  headers: {
    Authorization: 'Bearer yourapikey'
  }
}

const request = https.get(options, (res) => {
});
```

> Make sure to replace `yourapikey` with your API key.

Blockery uses API keys to allow access to the API. You can obtain a new Blockery API key by registering your company at our [developer portal](https://app.blockery.io).

Blockery expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer yourapikey`

<aside class="notice">
You must replace <code>yourapikey</code> with an API key registered to your organization.
</aside>
