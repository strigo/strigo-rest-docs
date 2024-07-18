---
weight: 140
---

# On Demand Course Enrollments

Enrollments represent single, learner-specific access definitions to on demand courses.

## The Enrollment Resource

### Attributes:

<aside class="notice">
Some of the following time attributes only exist once the enrollment was started.
</aside>

| Attribute         | Type     | Description                                                                                                                   |
|-------------------|----------|-------------------------------------------------------------------------------------------------------------------------------|
| `id`              | String   | The enrollments's unique identifier.                                                                                          |
| `course_id`       | String   | The on-demand course's unique ID the enrollment belongs to.                                                                   |
| `email`           | String   | The email of the learner.                                                                                                     |
| `status`          | String   | The current status of the enrollment (`enrolled`, `started`, `expired`, ...)                                                  |
| `enrolled_at`     | Datetime | The time in which the learner was enrolled.                                                                                   |
| `started_at`      | Datetime | The time in which the learner started the course.                                                                             |
| `expired_at`      | Datetime | The time in which the enrollment expired.                                                                                     |
| `finished_at`     | Datetime | The time in which the enrollment was finished.                                                                                |
| `inactivated_at`  | Datetime | The time in which the enrollment became inactive.                                                                             |
| `stopped_at`      | Datetime | The time in which the enrollment was stopped.                                                                                 |
| `paused_at`       | Datetime | The time in which the enrollment was paused.                                                                                  |
| `end_date`        | Datetime | The designated time for the enrollment to end.                                                                                |
| `first_activity`  | Datetime | The time in which the learner was first active in the course.                                                                 |
| `exercises`       | List     | The exercises for this enrollment (see [exercises](#workspace-exercises)).                                                    |
| `expiration_date` | Datetime | A fixed deadline. Regardless of when a student starts, their access to the course will end on this specific date (ISO8601).   |
| `timezone`        | String   | The timezone in which the expiration date is set to.See [timezone list](https://nodatime.org/TimeZones), Default is `Etc/UTC` |
| `active_time_left`        | Number   | The remaining activity time left for the enrollment (in minutes) |
| `enrollment_time_left`        | Number   | The remaining time left until the enrollment end date (in minutes) |

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
          "finished_at": "2018-09-20T10:39:35.425Z"
        },
        {
          "id": "BSY4hBSTGYfpXzN5G",
          "title": "Databases Overview",
          "status": "OPEN"
        }
      ],
			"active_time_left": 627,
			"enrollment_time_left": 155705
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

| Attribute         | Type     | Required | Description                                                                                                                   |
|-------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------|
| `course_id`       | String   | Yes      | The course's unique identifier.                                                                                               |
| `enrollment_id`   | String   | Yes      | The enrollment's unique identifier.                                                                                           |
| `expiration_date` | Datetime | No       | A fixed deadline. Regardless of when a student starts, their access to the course will end on this specific date (ISO8601).   |
| `timezone`        | String   | No       | The timezone in which the expiration date is set to.See [timezone list](https://nodatime.org/TimeZones), Default is `Etc/UTC` |

## Enroll a learner

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

> Request Example with expiration date

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand/NFdFJBSwwA8BrSpxk/enrollments" \
    -d @- <<EOF
    {
      "email":"me@strigo.io"
      "expiration_date": "2023-10-14T10:30:00.000Z",
      "timezone": "Europe/Paris"
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
  "status": "enrolled",
  "expiration_date": "2023-10-14T10:30:00.000Z",
  "timezone": "Europe/Paris"
}
```

### Usage

Enroll a learner to an on-demand course.

`POST "/ondemand/:course_id/enrollments"`

### URL Parameters

| Attribute   | Type   | Required | Description                     |
|-------------|--------|----------|---------------------------------|
| `course_id` | String | Yes      | The course's unique identifier. |

### BODY Parameters

| Attribute         | Type     | Required | Description                                                                                                                   |
|-------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------|
| `email`           | String   | Yes      | The email of the learner to invite.                                                                                           |
| `expiration_date` | Datetime | No       | A fixed deadline. Regardless of when a student starts, their access to the course will end on this specific date (ISO8601).   |
| `timezone`        | String   | No       | The timezone in which the expiration date is set to.See [timezone list](https://nodatime.org/TimeZones), Default is `Etc/UTC` |

## Modify an enrollment

> Request Example for explicit enrollment expiration

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
  "result": "success",
  "data": {
    "id": "d2iRTXOp8UcxvST",
    "course_id": "XYZ3uityordf66XQ",
    "email": "me18@strigo.io",
    "status": "expired",
    "enrolled_at": "2023-10-08T08:54:31.624Z",
    "expired_at": "2023-10-08T08:54:41.686Z",
    "exercises": []
  }
}
```

> Request Example for modifying expiration date

```shell
$ curl -X PATCH \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand/NFdFJBSwwA8BrSpxk/enrollments/9hQ5zitwbZh4zrga8" \
    -d @- <<EOF
    {
      "expiration_date": "2024-10-14T10:30:00.000Z",
      "timezone": "America/Los_Angeles"
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
  "status": "enrolled",
  "expiration_date": "2024-10-14T10:30:00.000Z",
  "timezone": "America/Los_Angeles"
}
```

### Usage

Modify an existing enrollment.

`PATCH "/ondemand/:course_id/enrollments/:enrollment_id"`

### URL Parameters

| Attribute       | Type   | Required | Description                         |
|-----------------|--------|----------|-------------------------------------|
| `course_id`     | String | Yes      | The course's unique identifier.     |
| `enrollment_id` | String | Yes      | The enrollment's unique identifier. |

### BODY Parameters

| Attribute         | Type     | Required | Description                                                                                                                   |
|-------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------|
| `status`          | String   | No       | The status to set the enrollment to (`expired`)                                                                               |
| `expiration_date` | Datetime | No       | A fixed deadline. Regardless of when a student starts, their access to the course will end on this specific date (ISO8601).   |
| `timezone`        | String   | No       | The timezone in which the expiration date is set to.See [timezone list](https://nodatime.org/TimeZones), Default is `Etc/UTC` |

<aside class="notice">
You can currently only patch enrollments to expire them.
</aside>

## Unenroll a learner

> Request Example

```shell
$ curl -X DELETE \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand/NFdFJBSwwA8BrSpxk/enrollments/9hQ5zitwbZh4zrga8"
```

> Response Example

```text
204 No Content
```

### Usage

Unenroll a previously enrolled learner.

<aside class="notice">
You can only delete enrollments in `enrolled` state.
</aside>

<aside class="notice">
You can also delete an enrollment by providing the url-encoded email of a learner instead of providing the enrollment ID.
</aside>

`DELETE "/ondemand/:course_id/enrollments/:enrollment_id"`

| Attribute       | Type   | Required | Description                                                            |
|-----------------|--------|----------|------------------------------------------------------------------------|
| `course_id`     | String | Yes      | The course's unique identifier.                                        |
| `enrollment_id` | String | Yes      | The enrollment's unique identifier (or leaner email. See note above.). |

## Enroll multiple learners

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand/NFdFJBSwwA8BrSpxk/enrollments/batch" \
    -d @- <<EOF
    {
      "emails":["me@strigo.io", "not_me@strigo.io"]
    }
EOF
```

> Successful Response Example

```json
[
  {
    "course_id": "NFdFJBSwwA8BrSpxk",
    "email": "me@strigo.io",
    "enrolled_at": "2018-10-28T08:14:55.743Z",
    "id": "yvTSaihvDRs7Kukeq",
    "status": "enrolled"
  },
  {
    "course_id": "NFdFJBSwwA8BrSpxk",
    "email": "not_me@strigo.io",
    "enrolled_at": "2018-10-28T08:14:55.743Z",
    "id": "avTSaihvDRs7Kukew",
    "status": "enrolled"
  }
]
```

> Request Example with expiration date

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand/NFdFJBSwwA8BrSpxk/enrollments/batch" \
    -d @- <<EOF
    {
      "emails":["me@strigo.io", "not_me@strigo.io"],
       "expiration_date": "2023-10-14T10:30:00.000Z",
       "timezone": "Asia/Jayapura"
    }
EOF
```

> Successful Response Example

```json
[
  {
    "course_id": "NFdFJBSwwA8BrSpxk",
    "email": "me@strigo.io",
    "enrolled_at": "2018-10-28T08:14:55.743Z",
    "id": "yvTSaihvDRs7Kukeq",
    "status": "enrolled",
    "expiration_date": "2023-10-14T10:30:00.000Z",
    "timezone": "Asia/Jayapura"
  },
  {
    "course_id": "NFdFJBSwwA8BrSpxk",
    "email": "not_me@strigo.io",
    "enrolled_at": "2018-10-28T08:14:55.743Z",
    "id": "avTSaihvDRs7Kukew",
    "status": "enrolled",
    "expiration_date": "2023-10-14T10:30:00.000Z",
    "timezone": "Asia/Jayapura"
  }
]
```

> Partial Success Response Example

```json
{
  "result": "failure",
  "error": {
    "message": "Could not enroll users",
    "type": "EnrollmentsCreateFailure",
    "errors": [
      {
        "type": "EnrollmentCreateFailure",
        "value": "me@strigo.io",
        "message": "User with provided email address has been already enrolled for the course"
      }
    ]
  },
  "data": [
    {
      "course_id": "NFdFJBSwwA8BrSpxk",
      "email": "not_me@strigo.io",
      "enrolled_at": "2018-10-28T08:14:55.743Z",
      "id": "avTSaihvDRs7Kukew",
      "status": "enrolled"
    }
  ]
}
```

### Usage

Enroll multiple learners to an on-demand course.

`POST "/ondemand/:course_id/enrollments/batch"`

### URL Parameters

| Attribute   | Type   | Required | Description                     |
|-------------|--------|----------|---------------------------------|
| `course_id` | String | Yes      | The course's unique identifier. |

### BODY Parameters

| Attribute         | Type     | Required | Description                                                                                                                   |
|-------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------|
| `emails`          | List     | Yes      | A list of learner emails to invite.                                                                                           |
| `expiration_date` | Datetime | No       | A fixed deadline. Regardless of when a student starts, their access to the course will end on this specific date (ISO8601).   |
| `timezone`        | String   | No       | The timezone in which the expiration date is set to.See [timezone list](https://nodatime.org/TimeZones), Default is `Etc/UTC` |

