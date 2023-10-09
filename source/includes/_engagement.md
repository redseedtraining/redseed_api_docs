# Engagement

Engagement is the percentage of active training at a Location.

## Engagement Attributes

Attribute | Type | Description
--------- | ------- | -----------
`location` | Location resource | The location resource
`NotStarted` | integer | The number of enrollments that are Not Started
`Training` | integer | The number of enrollments that are have a status of Training
`Inactive` | integer | The number of enrollments that have a status of Inactive
`Completed` | integer | The number of enrollments that have been completed
`Total` | integer | The total number of enrollments
`Engagement` | ratio | The ratio of enrollments that are training OR Completed

## Getting Engagement
```shell
curl --location --request GET 'https://api.redseed.me/api/v0/engagement/<location_id>' \
--header 'Authorization: Bearer <YOUR_API_TOKEN>'



```
> The above command returns a JSON response structured like this:

```json
{
    "location": {
        "id": 508798981,
        "status": "ACTIVE",
        "description": "Red Retail",
        "code": "RED88",
        "dateCreatedAt": "2023-02-13T23:30:00.000000Z",
        "dateUpdatedAt": "2023-02-13T23:30:00.000000Z"
    },
    "NotStarted": 16,
    "Training": 31,
    "Inactive": 89,
    "Completed": 74,
    "Total": 210,
    "Engagement": 0.5
}

```
This endpoint is used to fetch a list of users. It returns a JSON object that includes an array of user resources.


### HTTP Requests
`
GET https://api.redseed.me/api/v0/engagement
`

`
GET https://api.redseed.me/api/v0/engagement/<location_id>
`


### URL Parameters

Parameter | Description
--------- | -----------
`location_id` | The location to retrieve engagement for. if no location is specified, the client's top location will be used.
