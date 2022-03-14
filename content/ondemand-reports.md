---
weight: 115
---


# On Demand Course Question Reports

This data represents all workspaces question results that related to a specific ondemand course.

### Attributes:

Attribute                   | Type     | Description
---------                   | -------  | -------
`course_id`                 | String   | A unique identifier of the course.



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

`GET "/ondemand-courses/:course_id/workspaces/reports/questions"`

### URL Parameters

Attribute      | Type    | Required | Description
---------      | ------- | -------  | -------
`course_id`    | String  | Yes      | The course's unique identifier.



