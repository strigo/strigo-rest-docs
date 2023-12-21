---
weight: 115
---

# Event Reports

## Questions report

This data represents all workspaces question results that related to a specific event.

### Attributes:

| Attribute  | Type   | Description                       |
|------------|--------|-----------------------------------|
| `event_id` | String | A unique identifier of the event. |

### URL Parameters

| Attribute  | Type   | Required | Description                    |
|------------|--------|----------|--------------------------------|
| `event_id` | String | Yes      | The event's unique identifier. |

### Query Parameters

| Attribute | Type   | Required | Description                                                 |
|-----------|--------|----------|-------------------------------------------------------------|
| `output`  | String | No       | The desired output type (`json`, `csv`). Default is `json`. |

### Usage

Lists all workspaces for an event.

`GET "/events/:event_id/reports/questions"`


> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events/${EVENT_ID}/reports/questions"
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
  }
]
```

____________________________________________

## Lab Challenges report

This data represents all workspaces question results that related to a specific event.

### Attributes:

| Attribute  | Type   | Description                       |
|------------|--------|-----------------------------------|
| `event_id` | String | A unique identifier of the event. |

### URL Parameters

| Attribute  | Type   | Required | Description                    |
|------------|--------|----------|--------------------------------|
| `event_id` | String | Yes      | The event's unique identifier. |

### Query Parameters

| Attribute | Type   | Required | Description                                                 |
|-----------|--------|----------|-------------------------------------------------------------|
| `output`  | String | No       | The desired output type (`json`, `csv`). Default is `json`. |

### Usage

Lists all workspaces for an event.

`GET "/events/:event_id/reports/lab-challenges"`


> JSON Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events/${EVENT_ID}/reports/lab-challenges?output=json"
```

> Response Example

```json
{
  "result": "success",
  "data": [
    {
      "eventId": "45f2305650328ac7afd34a61",
      "eventName": "Erlich Bachman's new event",
      "workspaceId": "ymo45j5QknKEopgkJ",
      "email": "erlich.bachman@pp.io",
      "labChallengeTitle": "failing challenge",
      "validationResultTimestamp": "2023-11-21T09:43:14.423Z",
      "validationResult": "FAILURE"
    },
    {
      "eventId": "45f2305650328ac7afd34a61",
      "eventName": "Erlich Bachman's new event",
      "workspaceId": "ymo45j5QknKEopgkJ",
      "email": "erlich.bachman@pp.io",
      "labChallengeTitle": "#Example command that writes to stderr >&2",
      "validationResultTimestamp": "2023-11-21T09:43:59.285Z",
      "validationResult": "FAILURE"
    },
    {
      "eventId": "45f2305650328ac7afd34a61",
      "eventName": "Erlich Bachman's new event",
      "workspaceId": "ymo45j5QknKEopgkJ",
      "email": "erlich.bachman@pp.io",
      "labChallengeTitle": "successful challenge",
      "validationResultTimestamp": "2023-11-21T09:44:29.297Z",
      "validationResult": "SUCCESS"
    }
  ]
}
```

> CSV Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: text/csv" \
    -H "Content-Type: text/csv" \
    "https://app.strigo.io/api/v1/events/${EVENT_ID}/reports/lab-challenges?output=csv"
```

> Response Example

```csv
"Event Id","Event name","Enrollment Id","Course name","Validation timestamp","Email address","Lab challenge title","Result"
"45f2305650328ac7afd34a61","Erlich Bachman's new event","ymo45j5QknKEopgkJ",,"2023-11-21T09:43:14.423Z","hidday@strigo.io","failing challenge","FAILURE"
"45f2305650328ac7afd34a61","Erlich Bachman's new event","ymo45j5QknKEopgkJ",,"2023-11-21T09:43:59.285Z","hidday@strigo.io","# Example command that writes to stderr >&2 echo ""This is standard error (stderr)""","FAILURE"
"45f2305650328ac7afd34a61","Erlich Bachman's new event","ymo45j5QknKEopgkJ",,"2023-11-21T09:44:29.297Z","hidday@strigo.io","successfull challenge","SUCCESS"
```

____________________________________________

## User activity report

Lists event's user activity sessions.

### Attributes:

| Attribute  | Type   | Required | Description                       |
|------------|--------|----------|-----------------------------------|
| `event_id` | String | yes      | A unique identifier of the event. |
| `from`     | Date   | no       | Start date to filter activity by. | 
| `to`       | Date   | no       | End date to filter activity by.   | 

#### `from` - defaults to one month ago.

#### `to` - defaults to current request execution time.

### URL Parameters

| Attribute  | Type   | Required | Description                    |
|------------|--------|----------|--------------------------------|
| `event_id` | String | Yes      | The event's unique identifier. |

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
    "https://app.strigo.io/api/v1/events/${event_id}/reports/user-activity" \
    -d @- <<EOF
    {
      "from":"2022-10-07T15:10:52.934Z",
      "to": "2022-11-06T15:10:52.934Z"
    }
EOF
```

> Response Example

```json
{
  "result": "success",
  "data": [
    {
      "eventId": "635xxxxx0273addadxxxxxxx",
      "workspaceId": "roxxxxnphJohxxxxx",
      "name": "Bertram Gilfoyle",
      "email": "gilfoyle@pp.io",
      "role": "host",
      "status": "done",
      "startedAt": "2022-10-31T13:37:21.150Z",
      "sessions": [
        {
          "sessionStartTime": "2022-10-31T13:37:22.784Z",
          "sessionEndTime": "2022-10-31T13:41:45.386Z",
          "sessionDurationInSeconds": 262.602
        },
        {
          "sessionStartTime": "2022-10-31T14:31:01.863Z",
          "sessionEndTime": "2022-10-31T14:33:22.659Z",
          "sessionDurationInSeconds": 140.796
        }
      ],
      "totalSessionTime": 403.39799999999997,
      "from": "2022-10-07T15:10:52.934Z",
      "to": "2022-11-06T15:10:52.934Z"
    },
    {
      "eventId": "635xxxxx0273addadxxxxxxx",
      "workspaceId": "yyyYqh65taB3yyyy",
      "name": "Dinesh Chugtai",
      "email": "dinesh@pp.io",
      "role": "student",
      "status": "done",
      "startedAt": "2022-10-31T13:37:50.280Z",
      "sessions": [
        {
          "sessionStartTime": "2022-10-31T13:37:50.753Z",
          "sessionEndTime": "2022-10-31T13:46:22.528Z",
          "sessionDurationInSeconds": 511.775
        },
        {
          "sessionStartTime": "2022-10-31T14:31:07.156Z",
          "sessionEndTime": "2022-10-31T14:32:07.156Z",
          "sessionDurationInSeconds": 60
        },
        {
          "sessionStartTime": "2022-10-31T15:21:15.918Z",
          "sessionEndTime": "2022-10-31T15:22:15.918Z",
          "sessionDurationInSeconds": 60
        }
      ],
      "totalSessionTime": 631.775,
      "from": "2022-10-07T15:10:52.934Z",
      "to": "2022-11-06T15:10:52.934Z"
    }
  ]
}
```
