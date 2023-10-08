---
weight: 115
---

# On Demand Course Reports

## Questions report

This data represents all workspaces question results that related to a specific ondemand course.

### Attributes:

| Attribute   | Type   | Description                                                |
|-------------|--------|------------------------------------------------------------|
| `course_id` | String | A unique identifier of the course.                         |
| `output`    | String | The desired output type (`json`, `csv`). Default is `json`.|


### URL Parameters

| Attribute   | Type   | Required | Description                     |
|-------------|--------|----------|---------------------------------|
| `course_id` | String | Yes      | The course's unique identifier. |

### Query Parameters

| Attribute | Type   | Required | Description                                                 |
|-----------|--------|----------|-------------------------------------------------------------|
| `output`  | String | No       | The desired output type (`json`, `csv`). Default is `json`. |

### Usage

Lists all workspaces for an ondemand course.

`GET "/ondemand-courses/:course_id/reports/questions?output=json"`

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand-courses/${course_id}/reports/questions?output=json"
```

> Response Example

```json
[
  {
    "courseName": "Wrong answers only",
    "completionTimestamp": "2022-03-06T16:00:27.381Z",
    "email": "oleg.the.great+1234@viking.io",
    "questionNumber": 1,
    "questionTitle": "Kievan Rus",
    "question": "Who was Oleg?",
    "submittedNumber": 1,
    "submitted": "Software Engineer",
    "isCorrect": false
  }
]
```

_________________________________

## Lab Challenges report

This data represents all workspaces question results that related to a specific ondemand course.

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

Lists all workspaces for an ondemand course.

`GET "/ondemand-courses/:course_id/reports/lab-challenges"`

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand-courses/${course_id}/reports/lab-challenges?output=json"
```

> Response Example

```json
{
  "result": "success",
  "data": [
    {
      "courseId": "eb917a943d6d0365784e8779",
      "courseName": "Lab challenges",
      "enrollmentId": "6578571c59421c82c1f5a44f",
      "workspaceId": "pCFr9a6HzeEfKAm4a",
      "email": "erlich@strigo.io",
      "labChallengeTitle": "successfull challenge",
      "validationResultTimestamp": "2023-12-12T12:53:41.912Z",
      "validationResult": "SUCCESS"
    },
    {
      "courseId": "eb917a943d6d0365784e8779",
      "courseName": "Lab challenges",
      "enrollmentId": "657870b2b6f436010adcf866",
      "workspaceId": "EZvCvFwWmQREii4Tr",
      "email": "erlichbachman@pp.com",
      "labChallengeTitle": "failing challenge",
      "validationResultTimestamp": "2023-12-17T12:14:20.438Z",
      "validationResult": "FAILURE"
    },
    {
      "courseId": "eb917a943d6d0365784e8779",
      "courseName": "Lab challenges",
      "enrollmentId": "657870b2b6f436010adcf866",
      "workspaceId": "EZvCvFwWmQREii4Tr",
      "email": "erlichbachman@pp.com",
      "labChallengeTitle": "# Example command that writes to stderr >&2",
      "validationResultTimestamp": "2023-12-17T12:14:45.443Z",
      "validationResult": "FAILURE"
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
    "https://app.strigo.io/api/v1/ondemand-courses/${course_id}/reports/lab-challenges?output=csv"
```

> Response Example

```csv
"Course Id","Course name","Enrollment Id","Course name","Validation timestamp","Email address","Lab challenge title","Result"
"eb917a943d6d0365784e8779","Lab challenges","pCFr9a6HzeEfKAm4a","6578571c59421c82c1f5a44f","2023-12-12T12:53:41.912Z","erlich@strigo.io","successfull challenge","SUCCESS"
"eb917a943d6d0365784e8779","Lab challenges","EZvCvFwWmQREii4Tr","657870b2b6f436010adcf866","2023-12-17T12:14:20.438Z","erlich@pp.com","failing challenge","FAILURE"
"eb917a943d6d0365784e8779","Lab challenges","EZvCvFwWmQREii4Tr","657870b2b6f436010adcf866","2023-12-17T12:14:45.443Z","erlich@pp.com","# Example command that writes to stderr >&2","FAILURE"
"eb917a943d6d0365784e8779","Lab challenges","EZvCvFwWmQREii4Tr","657870b2b6f436010adcf866","2023-12-17T12:15:00.456Z","erlich@pp.com","# Example command that writes to stderr >&2","FAILURE"
```

_________________________

## User activity report

Lists on demand course user activity sessions.

### Attributes:

| Attribute   | Type   | Required | Description                       |
|-------------|--------|----------|-----------------------------------|
| `course_id` | String | yes      | A unique identifier of the event. |
| `from`      | Date   | no       | Start date to filter activity by. | 
| `to`        | Date   | no       | End date to filter activity by.   |

#### `from` - defaults to one month ago.

#### `to` - defaults to current request execution time.

### URL Parameters

| Attribute   | Type   | Required | Description                    |
|-------------|--------|----------|--------------------------------|
| `course_id` | String | Yes      | The event's unique identifier. |

### Body Parameters

| Attribute | Type | Required | Description                       |
|-----------|------|----------|-----------------------------------|
| `from`    | Date | no       | Start date to filter activity by. | 
| `to`      | Date | no       | End date to filter activity by.   | 

### Usage

Generate a report of attendees' user activity of the event.

`POST "/events/:event_id/reports/user-activity"`


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
