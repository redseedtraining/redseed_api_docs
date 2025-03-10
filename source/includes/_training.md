# Training

Training resources join Users to Courses. A training resource is created when a user is enrolled in a course. A training resource is deleted when a user is unenrolled from a course. 

## Training attributes


Attribute | Type | Description
--------- | ------- | -----------
`id` | integer | A unique and autoincrementing identifier for the training resource. Generated automatically.
`status` | text | 'Training', 'Coaching', 'NotStarted', 'Completed' - Training status.
`percentComplete` | integer | How far through the training the user is. This is a percentage value.
`seconds` | integer | How many seconds the trainee has spent on the training.
`external_launch_url` | string | Optional URL for launching external training content. Used for external courses.
`dateCreatedAt` | datetime | When the trainee was enrolled in the course.
`dateStartedAt` | datetime | When the trainee started the training.
`dateUpdatedAt` | datetime | When the training record was last updated.
`dateCompletedAt` | datetime | When the trainee completed the training.
`dateDueAt` | datetime | When the training is due to be completed.
`dateExpiresAt` | datetime | When the training expires. This is set when the training is created and is based on the course's expiry period.
`dateDeletedAt` | datetime | When the training record was deleted. This is set when the training is deleted.
`dateInactiveAt` | datetime | When the training will be - or was - marked as inactive. This is set when the training is marked as inactive.
`user` | UserResource | The trainee enrolled in this training.
`coach` | UserResource | The coach assigned to this training.
`course` | CourseResource | The course this training is for.
`courseVersion` | CourseVersionResource | The course version this training is for.
`media` | MediaResource | Any media associated with this training.
`tags` | Array of TagResources | Any tags associated with this training.

## Getting training resources
```shell
curl --location --request GET 'https://api.redseed.me/api/v0/training' \
--header 'Authorization: Bearer <YOUR_API_TOKEN>'

```
> The above command returns a JSON response structured like this:

```json
{
    "data": [
        // Training resource array
    ],
    "links": {
        "first": "https://api.redseed.me/api/v0/training?page=1",
        "last": "https://api.redseed.me/api/v0/training?page=9",
        "prev": null,
        "next": "https://api.redseed.me/api/v0/training?page=2"
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 9,
        "links": [
            // Pagination links
        ],
        "path": "https://api.redseed.me/api/v0/training",
        "per_page": 100,
        "to": 100,
        "total": 835
    }
}

```
This endpoint is used to fetch all training records. It returns a JSON object that includes an array of training resources.

Results are returned in pages of 1000 records. You can specify the page number to return using the `page` query parameter. If no page is specified, the first page will be returned.

### HTTP Requests
`
GET https://api.redseed.me/api/v0/training
`

`
GET https://api.redseed.me/api/v0/training/?course_id[]=<course_id>
`

`
GET https://api.redseed.me/api/v0/training/?course_id[]=<course_id>&course_id[]=<course_id>
`

`
GET https://api.redseed.me/api/v0/training/?user_id[]=<user_id>
`

`
GET https://api.redseed.me/api/v0/training/?coach_id[]=<coach_id>&course_id[]=<course_id>
`

`
GET https://api.redseed.me/api/v0/training/?location_id=<location_id>&course_id[]=<course_id>
`

`
GET https://api.redseed.me/api/v0/training/?external_ref_id[]=<external_ref_id>&external_ref_id[]=<external_ref_id>
`

`
GET https://api.redseed.me/api/v0/training/?tag[]=red&tag[]=blue
`

### URL Parameters

Parameter | Description
--------- | -----------
`page` | The page of results to retrieve. If no page is specified, the first page will be returned.
`location_id` | retrieve training for users at this location and its children.
`user_id[]` | retrieve training for this user. Supports multiple values.
`coach_id[]` | retrieve training records assigned to this coach. Supports multiple values.
`course_id[]` | retrieve training records for this course. Supports multiple values.
`external_ref_id[]` | retrieve training records for courses with these external reference IDs. Supports multiple values.
`tag[]` | retrieve training records that have these tags. Supports multiple values.


## Getting training details
```shell
curl --location --request GET 'https://api.redseed.me/api/v0/training/297065' \
--header 'Authorization: Bearer <YOUR_API_TOKEN>'
```

> The above command returns a JSON response structured like this:

```json
{
    "data": {
        "id": 297065,
        "status": "NotStarted",
        "percentComplete": 0,
        "seconds": 0,
        "external_launch_url": "https://www.example.org/training/123",
        "dateCreatedAt": "2017-09-15T01:24:53.000000Z",
        "dateStartedAt": null,
        "dateUpdatedAt": "2021-07-12T03:21:32.000000Z",
        "dateCompletedAt": null,
        "dateExpiresAt": null,
        "dateDeletedAt": null,
        "dateInactiveAt": null,
        "user": {
          // User Resource
        },
        "coach": {
          // User Resource
        },
        "course": {
          // Course Resource
        },
        "courseVersion": {
          // Course Version Resource
        },
        "media": {
          // Media Resource
        },
        //Array of Tag Resources
        "tags": [
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
}
```

This endpoint is used to fetch details about a specific training record. It returns a JSON object.

### HTTP Request
`
GET https://api.redseed.me/api/v0/training/<training_id>
`
### URL Parameters

Parameter | Description
--------- | -----------
`<training_id>` | The ID of the training record to retrieve.



## Enrolling a user in a course
```shell
curl --location --request POST 'https://api.redseed.me/api/v0/training' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer {MY_API_TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "user": {
        "id": 189814
    },
    "coach": {
        "id": 70152
    },
    "course": {
        "id": 2943
    },
    "external_launch_url": "https://www.example.org/1"
}'
```
> The above command returns JSON structured like this:

```json
{
    "id": 2083944,
    "status": "NotStarted",
    "percentComplete": 0,
    "seconds": 0,
    "external_launch_url": "https://www.example.org/1",
    "dateCreatedAt": "2023-06-26T02:41:27.000000Z",
    "dateStartedAt": null,
    "dateUpdatedAt": "2023-06-26T02:41:27.000000Z",
    "dateCompletedAt": null,
    "dateExpiresAt": null,
    "dateDeletedAt": null,
    "dateInactiveAt": null,
    "course": {
        "id": 2943,
        "name": "1. Opening the Sale",
        "status": "Active",
        "certificate": 0,
        "active_version": 1951,
        "description": null,
        "completion_time": 1015,
        "dateCreatedAt": "2021-04-27 16:48:22",
        "dateUpdatedAt": "2023-05-30 16:16:28",
        "dateReleasedAt": "2021-04-27 16:48:22"
    }
}
```

This endpoint is used to enroll a user in a course. It returns a JSON object.
### HTTP Request
`
POST https://api.redseed.me/api/v0/training
`

### Parameters
Attribute | Type | Required / Optional
--------- | --------- | ---------
`user.id` | integer | Required
`coach.id` | integer | Required
`course.id` | integer | Required
`external_launch_url` | string | Optional - URL for launching external training content


See <a href="#training-attributes">Training Attributes</a> for more information.

## Unenrolling a user from a course
```shell
curl --location --request DELETE 'https://api.redseed.me/api/v0/training/2083944' \
--header 'Authorization: Bearer <YOUR_API_TOKEN>'
```
Users can be unenrolled from a course by deleting the training record. This endpoint returns a 204 HTTP code.

### HTTP Request
`
DELETE https://api.redseed.me/api/v0/training/<training_id>
`

### URL Parameters
Parameter | Description
--------- | -----------
`<training_id>` | The id of the training record to remove.

## Getting self-enrollable courses
```shell
curl --location --request POST 'https://api.redseed.me/api/v0/self_enroll' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer {MY_API_TOKEN}' \
--header 'Content-Type: application/json' \
```
> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "id": 231852427,
            "name": "Red Course",
            "status": "Active",
            "certificate": 1,
            "activeVersion": {
                "id": 10724,
                "version_id": 3,
                "launch_url": "index.html",
                "schema_version": "xapi",
                "dateCreatedAt": "2024-01-31T03:16:59.000000Z",
                "dateUpdatedAt": "2024-01-31T03:16:59.000000Z"
            },
            "description": "A course about Red",
            "completion_time": 0,
            "dateCreatedAt": "2024-01-31T03:16:59.000000Z",
            "dateUpdatedAt":"2024-01-31T03:16:59.000000Z",
            "dateReleasedAt": null,
            "categories": [
                {
                    "id": 8908,
                    "name": "leadership"
                },
                {
                    "id": 8909,
                    "name": "product knowledge"
                }
            ]
        },
        {
            "id": 786489599,
            "name": "Blue Course",
            "status": "Active",
            "certificate": 1,
            "activeVersion": {
                "id": 10725,
                "version_id": 3,
                "launch_url": "index.html",
                "schema_version": "xapi",
                "dateCreatedAt": "2024-01-31T03:16:59.000000Z",
                "dateUpdatedAt": "2024-01-31T03:16:59.000000Z"
            },
            "description": "A course about Blue",
            "completion_time": 0,
            "dateCreatedAt": "2024-01-31T03:16:59.000000Z",
            "dateUpdatedAt": "2024-01-31T03:16:59.000000Z",
            "dateReleasedAt": "2024-01-31T03:16:59.000000Z",
            "categories": [
                {
                    "id": 8904,
                    "name": "coaching"
                },
                {
                    "id": 8905,
                    "name": "leadership"
                }
            ]
        }
    ]
}
```

This endpoint is used to fetch all courses that the user can self enroll themselves in. It returns a JSON object.
### HTTP Request
`
GET https://api.redseed.me/api/v0/self_enroll
`


## Self Enrolling in a course
```shell
curl --location --request POST 'https://api.redseed.me/api/v0/self_enroll/{course.id}' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer {MY_API_TOKEN}' \
--header 'Content-Type: application/json' \
```
> If the above command is successful it will return a single training JSON resource:

```json
{
    "id": 167,
    "status": "NotStarted",
    "percentComplete": null,
    "seconds": 0,
    "launch_url": "https:\/\/www.redseed.me\/training\/8392\/723938303\/1143945081\/167",
    "external_launch_url": "https://www.example.org/self-enroll/123",
    "dateCreatedAt": "2024-01-31T03:30:49.000000Z",
    "dateStartedAt": "2024-01-31T03:30:49.000000Z",
    "dateUpdatedAt": "2024-01-31T03:30:49.000000Z",
    "dateCompletedAt": null,
    "dateExpiresAt": null,
    "dateDeletedAt": null,
    "dateInactiveAt": "2024-02-14T03:30:49.000000Z",
    "user": {
        "id": 1143945081,
        "firstName": "Xzavier",
        "lastName": "Little",
        "email": "angeline162@example.com",
        "username": "160379",
        "code": "72461363",
        "type": "Trainee",
        "status": "Active",
        "marker": 0,
        "locale": "en_NZ",
        "dateLastLogin": null,
        "dateCreatedAt": "2024-01-31T03:30:49.000000Z",
        "dateUpdatedAt": "2024-01-31T03:30:49.000000Z",
        "dateArchivedAt": null,
        "dateActivityAt": "2024-01-31T03:30:49.000000Z"
    },
    "course": {
        "id": 723938303,
        "name": "Green Course",
        "status": "Active",
        "certificate": 1,
        "activeVersion": {
            "id": null,
            "version_id": 1,
            "launch_url": null,
            "schema_version": "RedSeed",
            "dateCreatedAt": null,
            "dateUpdatedAt": null
        },
        "description": "A course about green",
        "completion_time": 0,
        "dateCreatedAt": "2024-01-31T03:30:49.000000Z",
        "dateUpdatedAt": "2024-01-31T03:30:49.000000Z",
        "dateReleasedAt": "2024-01-31T03:30:49.000000Z"
    }
}
```

This endpoint is used to self enroll a user in a course. It returns a JSON Training resource object.

### HTTP Request
`POST https://api.redseed.me/api/v0/self_enroll/{course.id}`

<aside class="notice">
For external courses, the response will include an `external_launch_url` field. To set or modify this URL, use the training update endpoint after self-enrollment.
</aside>

## Updating a training record
```shell
curl --location --request PUT 'https://api.redseed.me/api/v0/training/297065' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer {MY_API_TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "status": "Training",
    "coach": {
        "id": 70152
    },
    "courseVersion": 1951,
    "external_launch_url": "https://www.example.org/updated",
    "dateStartedAt": "2024-01-31T03:30:49+0000",
    "dateCompletedAt": null,
    "dateExpiresAt": null,
    "dateDeletedAt": null,
    "tags": ["red", "blue", "green"]
}'
```

> The above command returns the updated training resource:

```json
{
    "data": {
        "id": 297065,
        "status": "Training",
        "percentComplete": 0,
        "seconds": 0,
        "external_launch_url": "https://www.example.org/updated",
        "dateCreatedAt": "2017-09-15T01:24:53.000000Z",
        "dateStartedAt": "2024-01-31T03:30:49.000000Z",
        "dateUpdatedAt": "2024-01-31T03:30:49.000000Z",
        "dateCompletedAt": null,
        "dateExpiresAt": null,
        "dateDeletedAt": null,
        "dateInactiveAt": null,
        "user": {
            // User Resource
        },
        "coach": {
            "id": 70152,
            // Rest of coach resource
        },
        "course": {
            // Course Resource
        },
        "courseVersion": {
            // Course Version Resource
        },
        "tags": [
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
}
```

This endpoint updates an existing training record. It returns the updated training resource.

### HTTP Request
`PUT https://api.redseed.me/api/v0/training/<training_id>`

### URL Parameters
Parameter | Description
--------- | -----------
`<training_id>` | The ID of the training record to update

### Body Parameters
Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
`status` | string | Required | Must be one of: 'Training', 'Coaching', 'NotStarted', or 'Completed'
`coach.id` | integer | Required | ID of an active coach in the client's organization
`courseVersion` | integer | Required | ID of a valid version for the training's course
`external_launch_url` | string | Optional | URL for launching external training content
`tags` | array of strings | Optional | Array of tag names to associate with the training
`dateStartedAt` | datetime | Optional | When the training was started. Format: ISO 8601 with timezone
`dateCompletedAt` | datetime | Optional | When the training was completed. Format: ISO 8601 with timezone
`dateExpiresAt` | datetime | Optional | When the training expires. Format: ISO 8601 with timezone
`dateDeletedAt` | datetime | Optional | When the training was deleted. Format: ISO 8601 with timezone

<aside class="notice">
Some attributes like user ID, course ID, created date, etc. cannot be modified through this endpoint. To change the user or course, delete the existing training and create a new one.
</aside>

<aside class="notice">
Tags must already exist. If a tag doesn't exist, it will be ignored.
</aside>
