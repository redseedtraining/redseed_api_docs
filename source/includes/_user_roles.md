# User roles

A RedSeed <a href="/#users">User</a> can be assigned a single user role. User roles can be used to segment RedSeed reports. User roles are NOT shared between RedSeed clients. User roles are not implemented by all RedSeed clients.

## User role attributes

Attribute | Type | Description
--------- | ------- | -----------
`id` | integer | A unique, auto-incrementing identifier for the user role.
`description` | text | Role description
`user_count` | integer | The number of users that have this role assigned. Includes archived users.

## Get a single user role

```shell
curl "https://api.redseed.me/api/v0/user_roles/{ID}" \
  -X GET \
  -H "Authorization: bearer {MY_API_TOKEN}"
```
```php
$curl = curl_init("https://api.redseed.me/api/v0/user_roles/{ID}");
curl_setopt($curl, CURLOPT_HTTPHEADER, [
  'Authorization: bearer {MY_API_TOKEN}'
]);
$response = curl_exec($curl);
```
```javascript
const redseedApi = require('redseedApi');
let api = redseedApi.authorize('{MY_API_TOKEN}');
let response = api.kittens.get('https://api.redseed.me/api/v0/user_roles/{ID}');
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 12,
    "description": "Store Manager",
    "user_count": 145
  }
}
```
### URL endpoint
`
https://api.redseed.me/api/v0/user_roles/{ID}
`
### URL Parameters

Parameter | Description
--------- | -----------
{ID} | The integer ID of the user role

### URL Query Parameters

None

<aside class="notice">
You must replace <code>{ID}</code> with the user role ID and <code>{MY_API_TOKEN}</code> with your personal API key.
</aside>

## Update user role

Not implemented via API, please contact RedSeed Support.

## Delete user role

Not implemented via API, please contact RedSeed Support.

## Restore user role

Not implemented via API, please contact RedSeed Support.

## Get multiple user roles

```shell
curl "https://api.redseed.me/api/v0/user_roles" \
  -X GET \
  -H "Authorization: bearer {MY_API_TOKEN}"
```
```php
$curl = curl_init("https://api.redseed.me/api/v0/user_roles");
curl_setopt($curl, CURLOPT_HTTPHEADER, [
  'Authorization: bearer {MY_API_TOKEN}'
]);
$response = curl_exec($curl);
```
```javascript
const redseedApi = require('redseedApi');
let api = redseedApi.authorize('{MY_API_TOKEN}');
let response = api.kittens.get('https://api.redseed.me/api/v0/user_roles');
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    { "id": 12, "description": "Store Manager", "user_count": 145 },
    { "id": 18, "description": "Sales Associate", "user_count": 392 }
  ],
  "links": {
    "first": "https://api.redseed.me/api/v0/user_roles?page=1",
    "last": "https://api.redseed.me/api/v0/user_roles?page=3",
    "prev": null,
    "next": "https://api.redseed.me/api/v0/user_roles?page=2"
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 3,
    "path": "https://api.redseed.me/api/v0/user_roles",
    "per_page": 100,
    "to": 100,
    "total": 250
  }
}
```
### URL endpoint
`
https://api.redseed.me/api/v0/user_roles
`
### URL Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
page_size | integer | Page size (default 100)
page | integer | Page number (1-based)
