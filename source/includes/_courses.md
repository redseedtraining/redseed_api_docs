# Courses

## Course Attributes

Attribute | Type | Description
--------- | ------- | -----------
`id` | integer | A unique and autoincrementing identifier for the Course which is generated by RedSeed automatically. | true
`name` | text | The course name
`status` | 'Active', 'Locked', 'Inactive', 'System' | The Course status. see User type. Used to set user abilities & permissions
`activeVersion` | Course version resource | The active version of the course. Courses may have multiple versions but only one may be active.
`description` | string | Course description
`completion_time` | integer | The median course completion time in seconds
`dateCreatedAt` | datetime | The datetime the course resource was created at
`dateUpdatedAt` | datetime | The datetime the course resource was last updated at
`dateReleasedAt` | datetime | The datetime the course resource was released at
`versions` | array of course versions | All Course version resources associated with this course, including the active course version.
`categories` | array of course categories | All Course categories that have been assigned to the course.


### Course type

Course type controls if a user can be enrolled in a course and if an existing enrollment is visible.

Parameter | Description
--------- | -----------
Active | Users can be enrolled in the course. Users with existing enrollments can complete the course.
Locked | Users cannot be enrolled in the course. Users with existing enrollments can complete the course.
Inactive | Users cannot be enrolled in the course. Existing Enrollments are not shown.


## Getting courses
```shell
curl --location --request GET 'https://api.redseed.me/api/v0/courses' \
--header 'Authorization: Bearer <YOUR_API_TOKEN>'

```
> The above command returns a JSON response structured like this:

```json
{
    "data": [
        {
            "id": 42694364,
            "name": "Red Course",
            "status": "Active",
            "description": "A course about red",
            "completion_time": 600,
            "dateCreatedAt": "2024-01-31T19:49:30.000000Z",
            "dateUpdatedAt": "2024-01-31T19:49:30.000000Z",
            "dateReleasedAt": "2024-01-31T19:49:30.000000Z",
            "versions": [
                {
                    "id": 14,
                    "version_id": 2,
                    "launch_url": "index.html",
                    "schema_version": "xapi",
                    "dateCreatedAt": "2024-01-31T19:49:30.000000Z",
                    "dateUpdatedAt": "2024-01-31T19:49:30.000000Z"
                }
            ]
        },
        {
            "id": 355230263,
            "name": "Blue Course",
            "status": "Active",
            "description": "A course about blue",
            "completion_time": 0,
            "dateCreatedAt": "2024-01-31T19:49:30.000000Z",
            "dateUpdatedAt": "2024-01-31T19:49:30.000000Z",
            "dateReleasedAt": "2024-01-31T19:49:30.000000Z",
            "versions": [
                {
                    "id": 15,
                    "version_id": 3,
                    "launch_url": "index.html",
                    "schema_version": "1.2",
                    "dateCreatedAt": "2024-01-31T19:49:30.000000Z",
                    "dateUpdatedAt": "2024-01-31T19:49:30.000000Z"
                }
            ]
        }
    ],
    "links": {
        ...
    },
    "meta": {
        ...
    }
}
```

This endpoint retrieves all course records. It returns a JSON object that includes an array of course resources.

Results are returned in pages of 100 records. You can specify the page number to return using the page query parameter. If no page is specified, the first page will be returned.

### HTTP Request Examples

Fetch all courses :<br>
`GET https://api.redseed.me/api/v0/courses`

Fetch page 2 of all courses :<br>
`GET https://api.redseed.me/api/v0/courses?page=2`

Fetch all courses with a course.type of Active :<br>
`GET https://api.redseed.me/api/v0/courses?status[]=Active`

Fetch course 2205 :<br>
`GET https://api.redseed.me/api/v0/courses/?course_id[]=2205`

Fetch courses 3306 & 3307 :<br>
`GET https://api.redseed.me/api/v0/courses/?course_id[]=3306&course_id[]=3307`


### Query Parameters

Parameter    | Default | Description
------------ | ------- | -----------
page         | 1       | The page of results to retrieve. If no page is specified, the first page will be returned.
course_id[]  | -       | retrieve this course resource. Supports multiple values.
status[]     | All     | retrive courses with this course type only. Supports multiple values.

<aside class="success">
If you select a single course via the course_id[] parameter the course resource will still be returned inside an array!
</aside>

## Getting course details
You can also fetch a single course resource like this :

```shell
curl --location --request GET 'https://api.redseed.me/api/v0/course/297065' \
--header 'Authorization: Bearer <YOUR_API_TOKEN>'
```

> The above command returns a JSON response structured like this:

```json
{
    "data": {
        "id": 205141907,
        "name": "Orange Course",
        "status": "Active",
        "description": "A course about oranges",
        "completion_time": 1230,
        "dateCreatedAt": "2017-09-15T01:24:53.000000Z",
        "dateUpdatedAt": "2017-09-15T01:24:53.000000Z",
        "dateReleasedAt": "2017-09-15T01:24:53.000000Z"
    }
}
```

This endpoint is used to fetch details about a specific course record. It returns a JSON object.

### HTTP Request
`
GET https://api.redseed.me/api/v0/course/<course.id>
`
### URL Parameters

Parameter | Description
--------- | -----------
`<course.id>` | The ID of the course resource to retrieve.


