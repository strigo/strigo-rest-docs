---
weight: 145
---

# On Demand Course Reports

## Enrollments report

This data represents all enrollments that related to a specific on demand course.

### Attributes:

| Attribute   | Type   | Description                                                 |
|-------------|--------|-------------------------------------------------------------|
| `course_id` | String | A unique identifier of the course.                          |
| `output`    | String | The desired output type (`json`, `csv`). Default is `json`. |

### URL Parameters

| Attribute   | Type   | Required | Description                     |
|-------------|--------|----------|---------------------------------|
| `course_id` | String | Yes      | The course's unique identifier. |

### Query Parameters

| Attribute | Type   | Required | Description                                                 |
|-----------|--------|----------|-------------------------------------------------------------|
| `output`  | String | No       | The desired output type (`json`, `csv`). Default is `json`. |

### Usage

Generates a report of all enrollments of the on demand course.

`GET "/ondemand-courses/:course_id/reports/enrollments"`

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand-courses/${course_id}/reports/enrollments?output=json"
```

> Response Example

```json
{
  "result": "success",
  "data": [
    {
      "course_id": "6363d3d399533fd52834c620",
      "course_name": "My on demand course",
      "enrollment_id": "65ae4e111113937279ef",
      "email": "monica@raviga.com",
      "name": "Monica Hall",
      "workspace_id": "9kxwQn3BvkGsFFT4Y",
      "enrolled_at": "2024-01-22T11:18:07.161Z",
      "started_at": "2024-01-22T12:24:53.411Z",
      "status": "finished",
      "exercises_finished": 0,
      "exercises_count": 2,
      "all_exercises_completed": false
    }
  ]
}
```

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: text/csv" \
    -H "Content-Type: text/csv" \
    "https://app.strigo.io/api/v1/ondemand-courses/${course_id}/reports/exercises?output=csv"
```

> Response Example

```csv
"course_id","course_name","enrollment_id","email","name","workspace_id","enrolled_at","started_at","exercises_finished","exercises_count","all_exercises_completed"
"6363d3d399533fd52834c620","My on demand course","65ae4e111113937279ef","monica@raviga.com","Monica Hall","9kxwQn3BvkGsFFT4Y","2024-01-22T11:18:07.161Z","2024-01-22T12:24:53.411Z","finished",0,2,false
```

_________________________


## Exercises report

This data represents all workspaces exercise results that related to a specific on demand course.

### Attributes:

| Attribute   | Type   | Description                                                 |
|-------------|--------|-------------------------------------------------------------|
| `course_id` | String | A unique identifier of the course.                          |
| `output`    | String | The desired output type (`json`, `csv`). Default is `json`. |

### URL Parameters

| Attribute   | Type   | Required | Description                     |
|-------------|--------|----------|---------------------------------|
| `course_id` | String | Yes      | The course's unique identifier. |

### Query Parameters

| Attribute | Type   | Required | Description                                                 |
|-----------|--------|----------|-------------------------------------------------------------|
| `output`  | String | No       | The desired output type (`json`, `csv`). Default is `json`. |

### Usage

Generates a report of all workspaces' exercise results of the on demand course.

`GET "/ondemand-courses/:course_id/reports/exercises"`

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand-courses/${course_id}/reports/exercises?output=json"
```

> Response Example

```json
{
  "result": "success",
  "data": [
    {
      "course_id": "eb917a943d6d0365784e8779",
      "course_name": "My course",
      "enrollment_id": "6578571c59421c82c1f5a44f",
      "email": "erlich@strigo.io",
      "name": "Erlich Bachman",
      "workspace_id": "J5SEv6sXeJQcSFwAG",
      "exercises_finished": 2,
      "exercises_count": 2,
      "all_exercises_completed": true,
      "exercise1_title": "First question",
      "exercise1_type": "question",
      "exercise1_result": "success",
      "exercise1_finished_at": "2023-11-21T09:43:59.285Z",
      "exercise2_title": "Second exercise",
      "exercise2_type": "exercise",
      "exercise2_result": "success",
      "exercise2_finished_at": "2023-11-21T09:59:59.285Z"
    }
  ]
}
```

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: text/csv" \
    -H "Content-Type: text/csv" \
    "https://app.strigo.io/api/v1/ondemand-courses/${course_id}/reports/exercises?output=csv"
```

> Response Example

```csv
"course_id","course_name","enrollment_id","email","name","workspace_id","exercises_finished","exercises_count","all_exercises_completed","exercise1_title","exercise1_type","exercise1_result","exercise1_finished_at","exercise2_title","exercise2_type","exercise2_result","exercise2_finished_at"
"eb917a943d6d0365784e8779","My course","6578571c59421c82c1f5a44f","erlich@strigo.io","Erlich Bachman","J5SEv6sXeJQcSFwAG",2,2,true,"First question","question","success","2023-11-21T09:43:59.285Z","Second exercise","exercise","failure","2023-11-21T09:59:59.285Z"
```

_________________________

## User activity report

Lists on demand course user activity sessions.

### Attributes:

| Attribute   | Type   | Required | Description                        |
|-------------|--------|----------|------------------------------------|
| `course_id` | String | yes      | A unique identifier of the course. |
| `from`      | Date   | no       | Start date to filter activity by.  | 
| `to`        | Date   | no       | End date to filter activity by.    |

#### `from` - defaults to one month ago.

#### `to` - defaults to current request execution time.

### URL Parameters

| Attribute   | Type   | Required | Description                     |
|-------------|--------|----------|---------------------------------|
| `course_id` | String | Yes      | The course's unique identifier. |

### Body Parameters

| Attribute | Type | Required | Description                       |
|-----------|------|----------|-----------------------------------|
| `from`    | Date | no       | Start date to filter activity by. | 
| `to`      | Date | no       | End date to filter activity by.   | 

### Usage

Generate a report of attendees' user activity of the on demand course.

`POST "/ondemand-courses/:course_id/reports/user-activity"`


> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand-courses/${course_id}/reports/user-activity" \
    -d @- <<EOF
    {
      "from": "2018-10-28T08:14:55.743Z",
      "to": "2022-11-07T08:14:55.743Z"
    }
EOF
```

> Response Example

```json
{
  "result": "success",
  "data": [
    {
      "courseId": "6363d3d399533fd52834c620",
      "workspaceId": "gF29ttALksgieTfYh",
      "enrollmentId": "63677b1f41cb30b50754d28e",
      "name": "Monica Hall",
      "email": "monica@raviga.com",
      "status": "started",
      "enrolledAt": "2022-11-06T09:15:11.572Z",
      "startedAt": "2022-11-06T09:15:32.425Z",
      "sessions": [
        {
          "sessionStartTime": "2022-11-06T09:15:32.468Z",
          "sessionEndTime": "2022-11-06T09:28:52.239Z",
          "sessionDurationInSeconds": 799.771
        }
      ],
      "totalSessionTime": 799.771,
      "from": "2018-10-28T08:14:55.743Z",
      "to": "2022-11-07T08:14:55.743Z"
    }
  ]
}
```
