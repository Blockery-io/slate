---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript

toc_footers:
  - <a href='https://app.blockery.io'>Sign-Up for a Blockery Account</a>

includes:
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

Blockery uses API keys to allow access to the API. You can register a new Blockery API key at our [developer portal](http://example.com/developers).

Blockery expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer yourapikey`

<aside class="notice">
You must replace <code>yourapikey</code> with an API key registered to your organization.
</aside>

# Resources

## Create a new Transaction

This endpoint is used in order to send assets from your organization wallet to an address which you specify.

### HTTP Request

`POST https://app.blockery.io/api/v1/transaction`

## Request Details

```python
import requests
r = requests.post("https://app.blockery.io/api/v1/transaction",
                  headers={"Authorization":"Bearer yourapikey"},
                  data={
                      "user_specified_id": "customid01",
                      "outputs": [
                          {
                              "assets": [
                                  {"name": "blockery", "policy_id": "3e3fa92bedc164c008a30fbc61d3d1fda9fa7137ab673e8237190aad", "quantity": 100}
                              ],
                              "lovelace_amount": 200000,
                              "receive_address": "addr_test1qz5atj4zxa3h534z3j7e40nwds8g3lhs2ms9f0s8geufvcar5waft2yukqkmxksdgn0rxwtn2sy2tpheq5gcrhea6caqeakqum"
                          }
                      ]
                  }
                  )
```

```shell
curl -d '{"user_specified_id": "customid01", "outputs": [ { "assets": [ {"name": "blockery", "policy_id": "3e3fa92bedc164c008a30fbc61d3d1fda9fa7137ab673e8237190aad", "quantity": 100}], "lovelace_amount": 200000, "receive_address": "addr_test1qz5atj4zxa3h534z3j7e40nwds8g3lhs2ms9f0s8geufvcar5waft2yukqkmxksdgn0rxwtn2sy2tpheq5gcrhea6caqeakqum"}]}' -H "Authorization: Bearer yourapikey" -X POST https://app.blockery.io/api/v1/transaction
```

```javascript
fetch('https://app.blockery.io/api/v1/transaction', {
  method: 'POST',
  headers: {
    'content-type': 'application/json',
    'Authorization': 'Bearer yourapikey'
  },
  body: {
    "user_specified_id": "customid01",
    "outputs": [
      {
        "assets": [
          {"name": "blockery", "policy_id": "3e3fa92bedc164c008a30fbc61d3d1fda9fa7137ab673e8237190aad", "quantity": 100}
        ],
        "lovelace_amount": 200000,
        "receive_address": "addr_test1qz5atj4zxa3h534z3j7e40nwds8g3lhs2ms9f0s8geufvcar5waft2yukqkmxksdgn0rxwtn2sy2tpheq5gcrhea6caqeakqum"
      }
    ]
  }
});
```

> The above command returns JSON structured like this:

```json
  {
    "follow_up_id": "1QQvUKfn7KMiWdHIE7KS",
    "user_specified_id": "1"
  }
```

#### Body Structure

Field | Type | Description
--------- | ------- | -----------
user_specified_id | string | This id will follow the transaction through it's entire lifecycle and be returned in any success or error messaging. It's purpose is to allow users to track a transaction as it moves through their system passing in and out of blockery. The value is arbitrarily supplied by the user. It has no effect on business logic.
outputs | Output | Each output represents a "Transaction Output". The objects represent what people typically think of as a transaction on the blockchain.

#### Output Structure

Field | Type | Optional |  Description
--------- | ------- | ----------- | -----
assets | Asset | True | These are tokens which the user is moving our of their wallet.
lovelace_amount | Integer | Fuzzy |The number of lovelace to send in this output. Lovelace will always be included in an output even if you don't specify it here explicitly.  If you do not include a `lovelace_amount` in an Output, the system will automatically calculate and include the minimum amount necessary to send with your included assets.
receive_address | string | False | The destination address to send the assets and ada described in this Output.
<aside class="success">
Remember — You are not required to send `assets` in a transaction. But you must send something! Omitting assets and lovelace will result in validation failure.
</aside>

#### Assets Structure

Field | Type | Description
--------- | ------- | -----------
name | String | The name of the asset. Provide the utf-8 encoded version (ie. human readable)
policy_id | String | The policy id used to mint this asset
quantity | Integer | How any of the asset to send




### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'blockery'

api = Blockery::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import blockery

api = blockery.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const blockery = require('blockery');

let api = blockery.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'blockery'

api = Blockery::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import blockery

api = blockery.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const blockery = require('blockery');

let api = blockery.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

