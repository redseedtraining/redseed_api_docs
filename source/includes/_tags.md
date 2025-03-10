# Tags

Tags allow you to categorise and filter training records. You can create, retrieve, update, and delete tags through the API.

## Tag Attributes

Attribute | Type | Description
--------- | ------- | -----------
`id` | integer | A unique identifier for the tag
`name` | string | The unique name of the tag

## Getting Tags

```shell
curl --location --request GET 'https://api.redseed.me/api/v0/tags' \
--header 'Authorization: Bearer <YOUR_API_TOKEN>'
```

> The above command returns a JSON response structured like this:

```json
{
    "data": [
        {
            "id": 13,
            "name": "red"
        },
        {
            "id": 14,
            "name": "blue"
        },
        {
            "id": 16,
            "name": "green"
        }
    ]
}
```

This endpoint retrieves all tags for your account. It returns a JSON object that includes an array of tag resources.

### HTTP Request
`GET https://api.redseed.me/api/v0/tags`

## Creating a Tag

```shell
curl --location --request POST 'https://api.redseed.me/api/v0/tags' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer {MY_API_TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "project-alpha"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": 42,
    "name": "project-alpha"
}
```

This endpoint creates a new tag. It returns a JSON object containing the created tag resource.

### HTTP Request
`POST https://api.redseed.me/api/v0/tags`

### Body Parameters
Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
`name` | string | Required | The name of the tag

## Updating a Tag

```shell
curl --location --request PUT 'https://api.redseed.me/api/v0/tags/42' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer {MY_API_TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "project-beta"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": 42,
    "name": "project-beta"
}
```

This endpoint updates an existing tag. It returns a JSON object containing the updated tag resource.

### HTTP Request
`PUT https://api.redseed.me/api/v0/tags/{tag_id}`

### URL Parameters
Parameter | Description
--------- | -----------
`tag_id` | The ID of the tag to update

### Body Parameters
Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
`name` | string | Required | The new name for the tag

## Using Tags with Training Records

Tags can be used to categorise and filter training records. You can:

1. **Add tags when creating a training record**:
```json
{
    "user": {
        "id": 189814
    },
    "coach": {
        "id": 70152
    },
    "course": {
        "id": 2943
    },
    "tags": ["red", "blue", "green"]
}
```

2. **Update tags on an existing training record**:
```json
{
    "tags": ["red", "green"]
}
```

3. **Filter training records by tags**:
```
GET https://api.redseed.me/api/v0/training/?tag[]=red&tag[]=blue
```

<aside class="notice">
Tags must already exist. If a tag doesn't exist when adding it to a training record, the request will fail.
</aside>

<aside class="notice">
When updating tags on a training record, the existing tags will be replaced with the new list of tags provided.
</aside> 