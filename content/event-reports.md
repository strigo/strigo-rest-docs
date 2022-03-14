---
weight: 115
---


# Event Question Reports

This data represents all workspaces question results that related to a specific event.

### Attributes:

Attribute                   | Type     | Description
---------                   | -------  | -------
`event_id`                  | String   | A unique identifier of the event.



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
  },
]
```

### Usage

Lists all workspaces for an event.

`GET "/events/:event_id/workspaces/reports/questions"`

### URL Parameters

Attribute      | Type    | Required | Description
---------      | ------- | -------  | -------
`event_id`     | String  | Yes      | The event's unique identifier.



