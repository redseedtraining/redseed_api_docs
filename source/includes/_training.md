# Training

Training resources join Users to Courses. A training resource is created when a user is enrolled in a course. A training resource is deleted when a user is unenrolled from a course. 

## Training attributes


Attribute | Type | Description
--------- | ------- | -----------
`id` | integer | A unique and autoincrementing identifier for the training resource. Generated automatically.
`status` | text | 'Training', 'Coaching', 'NotStarted', 'Completed' - Training status.
`percentComplete` | integer | How far through the training the user is. This is a percentage value.
`seconds` | integer | How many seconds the trainee has spent on the training.
`dateCreatedAt` | datetime | When the trainee was enrolled in the course.
`dateStartedAt` | datetime | When the trainee started the training.
`dateUpdatedAt` | datetime | When the training record was last updated.
`dateCompletedAt` | datetime | When the trainee completed the training.
`dateExpiresAt` | datetime | When the training expires. This is set when the training is created and is based on the course's expiry period.
`dateDeletedAt` | datetime | When the training record was deleted. This is set when the training is deleted.
`dateInactiveAt` | datetime | When the training will be - or was - marked as inactive. This is set when the training is marked as inactive.
`user` | UserResource | The trainee enrolled in this training.
`coach` | UserResource | The coach assigned to this training.
`course` | CourseResource | The course this training is for.
`courseVersion` | CourseVersionResource | The course version this training is for.

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

### URL Parameters

Parameter | Description
--------- | -----------
`page` | The page of results to retrieve. If no page is specified, the first page will be returned.
`location_id` | retrieve training for users at this location and its children.
`user_id[]` | retrieve training for this user. Supports multiple values.
`coach_id[]` | retrieve training records assigned to this coach. Supports multiple values.
`course_id[]` | retrieve training records for this course. Supports multiple values.


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
        }
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
    }
}'
```
> The above command returns JSON structured like this:

```json
{
    "id": 2083944,
    "status": "NotStarted",
    "percentComplete": 0,
    "seconds": 0,
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