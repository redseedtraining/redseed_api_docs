# Pathways
Pathways consist of a group of courses. In general, a pathway will enroll trainees in a course after they have completed the previous course in the pathway. Pathways can be used to create a structured learning program for trainees.

## Pathway Attributes

Attribute | Type | Description
--------- | ------- | -----------
`id` | string | A uuid that uniquely identifies the pathway 
`name` | text | The name of the pathway
`description` | text | A description of the pathway
`status` | text | The status of the pathway. Can be 'Active' or 'Locked'
`dateCreatedAt` | datetime | The date the pathway was created.
`dateUpdatedAt` | datetime | The date the pathway was last updated.
`dateDeletedAt` | datetime | The date the pathway was deleted.
`enrollment_rules` | Enrollment Rule | Enrollment rule resources associated with this pathway.

## Enrollment Rules

Attribute | Type | Description
--------- | ------- | -----------
`id` | string | A uuid that uniquely identifies the pathway 
`position` | integer | This enrollment rules position / order
`type` | text | INITIAL or COMPLETE. Initial rules don't require a completed course. COMPLETE rules require a course to be completed.
`incomingCourse` | Course | The status of the pathway. Can be 'Active' or 'Locked'
`enrollCourse` | Course | The date the pathway was created.
`delay` | integer | Used to wait a number of days after the incoming Course has been completed
`created_at` | datetime | The date the enrollment rule was created.
`updated_at` | datetime | the date the enrollment rule was last updated.

## Getting pathways
```shell
curl --location --request GET 'https://api.redseed.me/api/v0/pathways' \
--header 'Authorization: Bearer <YOUR_API_TOKEN>'

```
> The above command returns a JSON response structured like this:

```json
{
    "data": [
        // Pathway resource array
    ],
    "links": {
        "first": "https://api.redseed.me/api/v0/pathways?page=1",
        "last": "https://api.redseed.me/api/v0/pathways?page=9",
        "prev": null,
        "next": "https://api.redseed.me/api/v0/pathways?page=2"
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 9,
        "links": [
            // Pagination links
        ],
        "path": "https://api.redseed.me/api/v0/pathways",
        "per_page": 100,
        "to": 100,
        "total": 835
    }
}
```

### HTTP Request
`
GET https://api.redseed.me/api/v0/pathways/?page=<page_number>
`
### URL Parameters

Parameter | Description
--------- | -----------
`<page_number>` | The page of results to retrieve. If no page is specified, the first page will be returned.

## Getting pathway details
```shell
curl --location --request GET 'https://api.redseed.me/api/v0/pathways/d6ad3424-ef9c-466c-b783-80a688645ce5' \
--header 'Authorization: Bearer <YOUR_API_TOKEN>'
```

> The above command returns a JSON response structured like this:

```json
{
    "data": {
        "id": "d6ad3424-ef9c-466c-b783-80a688645ce5",
        "name": "Test",
        "description": "test",
        "status": "Active",
        "dateCreatedAt": "2023-06-20T21:22:05.000000Z",
        "dateUpdatedAt": "2023-06-20T21:22:05.000000Z",
        "dateDeletedAt": null
    }
}
```

### HTTP Request
`
GET https://api.redseed.me/api/v0/pathways/<pathway_id>
`
### URL Parameters

Parameter | Description
--------- | -----------
`<pathway_id>` | The UUID of the pathway record to retrieve.

## Enrolling a user in a pathway
```shell
curl --location --request POST 'https://api.redseed.me/api/v0/user_pathways' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer <YOUR_API_TOKEN>' \
--header 'Content-Type: application/json' \
--data-raw '{
    "user": {
        "id": 189814
    },
    "pathway": {
        "uuid":"4f858f3e-8337-4220-bd61-cc72f3cc4cf1"
    }
}'

```
> The above command returns a JSON response structured like this:

```json
{
    "id": 132447,
    "status": "Active",
    "trainingCompleted": 0,
    "trainingTotal": 3,
    "dateCreatedAt": "2023-06-29T02:00:49.000000Z",
    "dateUpdatedAt": "2023-06-29T02:00:50.000000Z",
    "dateDeletedAt": null,
    "pathway": {
        "id": "4f858f3e-8337-4220-bd61-cc72f3cc4cf1",
        "name": "Coms demo pathway",
        "description": "Demo pathway that allows users to try out some of the communication modules for RedSeed.",
        "status": "Active",
        "dateCreatedAt": "2023-06-26T00:12:16.000000Z",
        "dateUpdatedAt": "2023-06-26T00:12:16.000000Z",
        "dateDeletedAt": null
    },
    "user": {
        "id": 189814,
        "firstName": "Test",
        "lastName": "API User",
        "email": "test.api1234@mail.com",
        "username": "test.api1234@mail.com",
        "code": "employee_code_1234",
        "type": "Trainee",
        "status": "Active",
        "marker": 1,
        "locale": "en_NZ",
        "dateLastLogin": null,
        "dateCreatedAt": "2023-06-21T22:31:30.000000Z",
        "dateUpdatedAt": "2023-06-21T22:31:30.000000Z",
        "dateArchivedAt": null,
        "dateActivityAt": null,
        "location": {
            "id": 11728,
            "status": "ACTIVE",
            "description": "Demo",
            "code": null,
            "dateCreatedAt": null,
            "dateUpdatedAt": "2023-06-28T12:00:50.000000Z"
        }
    }
}
```
### HTTP Request
`
POST https://api.redseed.me/api/v0/user_pathways
`

### Parameters
Attribute | Type | Required / Optional
--------- | --------- | ---------
`user.id` | integer | Required
`pathway.uuid` | string | Required

## Unenrolling a user from a pathway
```shell
curl --location --request DELETE 'https://api.redseed.me/api/v0/user_pathways/132447' \
--header 'Authorization: Bearer <YOUR_API_TOKEN>'
```
Users can be unenrolled from a pathway by deleting the user pathway record. This endpoint returns a 204 HTTP code.
### HTTP Request
`
DELETE https://api.redseed.me/api/v0/user_pathways/<user_pathway_id>
`

### URL Parameters
Parameter | Description
--------- | -----------
`<user_pathway_id>` | The id of the user pathway record to remove.