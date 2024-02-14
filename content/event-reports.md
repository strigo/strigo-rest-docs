---
weight: 115
---

# Event Reports

## Exercises report

This data represents all workspaces' exercise results that related to a specific event.

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

Generates a report of all workspaces' exercise results of the event.

`GET "/events/:event_id/reports/exercises"`


> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events/${event_id}/reports/exercises"
```

> Response Example

```json
[
  {
    "event_id": "45f2305650328ac7afd34a61",
    "event_name": "Erlich Bachman's new event",
    "email": "erlich@strigo.io",
    "name": "Erlich Bachman",
    "workspace_id": "J5SEv6sXeJQcSFwAG",
    "exercises_finished": 2,
    "exercises_count": 2,
    "all_exercises_completed": true,
    "exercise_1_title": "First question",
    "exercise_1_type": "question",
    "exercise_1_result": "success",
    "exercise_1_finished_at": "2023-11-21T09:43:59.285Z",
    "exercise_2_title": "Second exercise",
    "exercise_2_type": "exercise",
    "exercise_2_result": "success",
    "exercise_2_finished_at": "2023-11-21T09:59:59.285Z",
  }
]
```

> CSV Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: text/csv" \
    -H "Content-Type: text/csv" \
    "https://app.strigo.io/api/v1/events/${event_id}/reports/exercises?output=csv"
```

> Response Example

```csv
event_id,event_name,email,name,workspace_id,exercises_finished,exercises_count,all_exercises_completed,exercise_1_title,exercise_1_type,exercise_1_result,exercise_1_finished_at,exercise_2_title,exercise_2_type,exercise_2_result,exercise_2_finished_at
"45f2305650328ac7afd34a61","Erlich Bachman's new event","erlich@strigo.io","Erlich Bachman","J5SEv6sXeJQcSFwAG",2,2,true,"First question","question","success","2023-11-21T09:43:59.285Z","Second exercise","exercise","failure","2023-11-21T09:59:59.285Z"
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
