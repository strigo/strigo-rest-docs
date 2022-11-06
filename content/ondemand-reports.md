---
weight: 115
---


# On Demand Course Reports

## Questions report

This data represents all workspaces question results that related to a specific ondemand course.

### Attributes:

| Attribute   | Type   | Description                        |
|-------------|--------|------------------------------------|
| `course_id` | String | A unique identifier of the course. |

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand-courses/${course_id}/reports/questions"
```

> Response Example

```json
[
  {
      "courseName": "Wrong answers only",
      "completionTimestamp": "2022-03-06T16:00:27.381Z",
      "email": "oleg.mostepan+1234@strigo.io",
      "questionNumber": 1,
      "questionTitle": "Kievan Rus",
      "question": "Who was Oleg?",
      "submittedNumber": 1,
      "submitted": "Software Engineer at Strigo",
      "isCorrect": false
  },
]
```

### Usage

Lists all workspaces for an course.

`GET "/ondemand-courses/:course_id/reports/questions"`

### URL Parameters

| Attribute   | Type   | Required | Description                     |
|-------------|--------|----------|---------------------------------|
| `course_id` | String | Yes      | The course's unique identifier. |


## User activity report


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

| Attribute  | Type   | Required | Description                       |
|------------|--------|----------|-----------------------------------|
| `from`     | Date   | no       | Start date to filter activity by. | 
| `to`       | Date   | no       | End date to filter activity by.   | 

### Usage

Generate a report of attendees' user activity of the event.

`POST "/events/:event_id/reports/user-activity"`
