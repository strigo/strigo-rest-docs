---
weight: 140
---

# On Demand Course Enrollments

Enrollments represent single, student-specific access definitions to on demand courses.

## The Enrollment Resource

### Attributes:

<aside class="notice">
Some of the following time attributes only exist once the enrollment was started.
</aside>

Attribute        | Type     | Description
---------        | -------  | -------
`id`             | String   | The enrollments's unique identifier.
`course_id`      | String   | The on-demand course's unique ID the enrollment belongs to.
`email`          | String   | The email of the student.
`status`         | String   | The current status of the enrollment (`enrolled`, `started`, `expired`, ...)
`enrolled_at`    | Datetime | The time in which the student was enrolled.
`started_at`     | Datetime | The time in which the student started the course.
`expired_at`     | Datetime | The time in which the enrollment expired.
`finished_at`    | Datetime | The time in which the enrollment was finished.
`inactivated_at` | Datetime | The time in which the enrollment became inactive.
`stopped_at`     | Datetime | The time in which the enrollment was stopped.
`paused_at`      | Datetime | The time in which the enrollment was paused.
`end_date`       | Datetime | The designated time for the enrollment to end.
`first_activity` | Datetime | The time in which the student was first active in the course.
`exercises`      | List     | The exercises for this enrollment (see [exercises](#workspace-exercises)).



## Retrieve all enrollments

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand/nE5pDWGzFRRQ8uMrN/enrollments"
```

> Response Example

```json
[
  {
      "course_id": "NFdFJBSwwA8BrSpxk",
      "email": "me1@strigo.io",
      "enrolled_at": "2018-10-16T11:40:11.239Z",
      "id": "xK8cPmPYEuXwjxbu3",
      "started_at": "2018-10-16T11:40:27.929Z",
      "end_date": "2018-10-26T11:40:27.929Z",
      "status": "expired",
      "exercises": [
        {
          "id": "pB6H3XaTS2Tf53z3p",
          "title": "Introduction",
          "status": "DONE",
          "finished_at": "2018-09-20T10:39:35.425Z",
        },
        {
          "id": "BSY4hBSTGYfpXzN5G",
          "title": "Databases Overview",
          "status": "OPEN"
        }
      ]
  },
  {
      "course_id": "NFdFJBSwwA8BrSpxk",
      "email": "me2@strigo.io",
      "enrolled_at": "2018-10-18T14:09:38.832Z",
      "id": "9hQ5zitwbZh4zrga8",
      "status": "enrolled"
  }
]
```

### Usage

Lists all enrollments for the course, regardless of their status.

`GET "/ondemand/:course_id/enrollments"`


## Retrieve a single enrollment

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand/NFdFJBSwwA8BrSpxk/enrollments/9hQ5zitwbZh4zrga8"
```

> Response Example

```json
{
  "course_id": "NFdFJBSwwA8BrSpxk",
  "email": "me2@strigo.io",
  "enrolled_at": "2018-10-18T14:09:38.832Z",
  "id": "9hQ5zitwbZh4zrga8",
  "status": "enrolled"
}
```

### Usage

Get a single enrollment.

`GET "/ondemand/:course_id/enrollment/:enrollment_id"`

### URL Parameters

Attribute       | Type    | Required | Description
---------       | ------- | -------  | -------
`course_id`     | String  | Yes      | The course's unique identifier.
`enrollment_id` | String  | Yes      | The enrollment's unique identifier.


## Enroll a student

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand/NFdFJBSwwA8BrSpxk/enrollments" \
    -d @- <<EOF
    {
      "email":"me@strigo.io"
    }
EOF
```

> Response Example

```json
{
  "course_id": "NFdFJBSwwA8BrSpxk",
  "email": "me@strigo.io",
  "enrolled_at": "2018-10-28T08:14:55.743Z",
  "id": "yvTSaihvDRs7Kukeq",
  "status": "enrolled"
}
```

### Usage

Enroll a student to an on-demand course.

`POST "/ondemand/:course_id/enrollments"`

### URL Parameters

Attribute   | Type    | Required | Description
---------   | ------- | -------  | -------
`course_id` | String  | Yes      | The course's unique identifier.

### BODY Parameters

Attribute        | Type     | Required | Description
---------        | -------  | -------- | -------
`email`          | String   | Yes      | The email of the student to invite.


## Modify an enrollment

> Request Example

```shell
$ curl -X PATCH \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand/NFdFJBSwwA8BrSpxk/enrollments/9hQ5zitwbZh4zrga8" \
    -d @- <<EOF
    {
      "status": "expired"
    }
EOF
```

> Response Example

```json
{
  "course_id": "NFdFJBSwwA8BrSpxk",
  "email": "me@strigo.io",
  "enrolled_at": "2018-10-28T08:14:55.743Z",
  "started_at": "2018-10-16T11:40:27.929Z",
  "end_date": "2018-10-26T11:40:27.929Z",
  "id": "yvTSaihvDRs7Kukeq",
  "status": "expired"
}
```

### Usage

Modify an existing enrollment.

`PATCH "/ondemand/:course_id/enrollments/:enrollment_id"`

### URL Parameters

Attribute       | Type     | Required | Description
---------       | -------  | -------  | -------
`course_id`     | String   | Yes      | The course's unique identifier.
`enrollment_id` | String   | Yes      | The enrollment's unique identifier.

### BODY Parameters

Attribute           | Type     | Required | Description
---------           | -------  | -------  | -------
`status`            | String   | Yes      | The status to set the enrollment to (`expired`)

<aside class="notice">
You can currently only patch enrollments to expire them.
</aside>


## Unenroll a student

> Request Example

```shell
$ curl -X DELETE \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events/p3bdnrweEystFToCq"
```

> Response Example

```text
204 No Content
```


### Usage

Unenroll a previously enrolled student.

<aside class="notice">
You can only delete enrollments in `enrolled` state.
</aside>

`DELETE "/ondemand/:course_id/enrollments/:enrollment_id"`

Attribute       | Type     | Required | Description
---------       | -------  | -------  | -------
`course_id`     | String   | Yes      | The course's unique identifier.
`enrollment_id` | String   | Yes      | The enrollment's unique identifier.
