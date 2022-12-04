---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - users
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Welcome to the RedSed API You can use our API to access RedSeed API endpoints, which can get information on your users, training, courses and more.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```php
use Guzzle;

Guzzle connection example in header
YOUR_API_KEY
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('YOUR_API_KEY');
```

> Make sure to replace `YOUR_API_KEY` with your API key.

RedSeed uses API keys to allow access to our API. You can request a new RedSeed API key by contacting <a href='https://support.redseed.me'>RedSeed Support</a>.

RedSeed expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: YOUR_API_KEY`

<aside class="notice">
You must replace <code>YOUR_API_KEY</code> with your personal API key.
</aside>

# Requesting a token

https://laravel-guide.readthedocs.io/en/latest/passport/#requesting-tokens

