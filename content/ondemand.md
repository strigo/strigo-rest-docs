---
weight: 130
---


# On Demand Courses

## The On Demand Course Resource

### Attributes:

Attribute              | Type    | Description
---------              | ------- | -------
`id`                   | String  | The course's unique identifier.
`name`                 | String  | The name of the course.
`course_link`          | String  | The course's attendance link.
`class_id`             | String  | The class's unique ID the course is based on.
`external_id`          | String  | The user provided external ID of the course.
`days_limit`           | Number  | The number of the days each enrollment will be limited to.
`activity_hours_limit` | Number  | The number of work hours each enrollment will be limited to.
`public_access_token`  | String  | The course's public access token.
`status`               | String  | The status of the course (`online`, `offline`).

## Retrieve all courses

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "http://app.strigo.io/api/v1/ondemand"
```

> Response Example

```json
[
  {
    "activity_hours_limit": 10,
    "class_id": "hd3ALTaLAbhfzmBbf",
    "course_link": "https://app.strigo.io/training/ondemand/nE5pDWGzFRRQ8uMrN",
    "days_limit": 5,
    "external_id": "course1",
    "id": "nE5pDWGzFRRQ8uMrN",
    "name": "Elastic Stack for beginners",
    "public_access_token": "DQGT",
    "status": "online"
  }
]
```

### Usage

Lists all on demand courses for your organization, regardless of their status.

`GET "/ondemand"`


## Retrieve a single course

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "http://app.strigo.io/api/v1/ondemand/nE5pDWGzFRRQ8uMrN"
```

> Response Example

```json
{
  "activity_hours_limit": 10,
  "class_id": "hd3ALTaLAbhfzmBbf",
  "course_link": "https://app.strigo.io/training/ondemand/nE5pDWGzFRRQ8uMrN",
  "days_limit": 5,
  "external_id": "course1",
  "id": "nE5pDWGzFRRQ8uMrN",
  "name": "Elastic Stack for beginners",
  "public_access_token": "DQGT",
  "status": "online"
}
```

### Usage

Get a single on demand course.

`GET "/ondemand/:course_id"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`course_id`| String  | Yes      | The course's unique identifier.


## Create a course

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "http://app.strigo.io/api/v1/ondemand" \
    -d { \
      "name":"My Event", \
      "class_id": "hd3ALTaLAbhfzmBbf", \
      "days_limit": 5, \
      "activity_hours_limit": 10, \
      "status": "online", \
      "external_id": "course1" \
    }
```

> Response Example

```json
{
  "activity_hours_limit": 10,
  "class_id": "hd3ALTaLAbhfzmBbf",
  "course_link": "https://app.strigo.io/training/ondemand/i7gHDXnDzpRFQqFZP",
  "days_limit": 5,
  "external_id": "course1",
  "id": "i7gHDXnDzpRFQqFZP",
  "name": "ooo",
  "public_access_token": "MEWD",
  "status": "online"
}
```

### Usage

Create a new event.

`POST "/ondemand"`

### BODY Parameters

Attribute              | Type    | Required | Description
---------              | ------- |  ------- | -------
`name`                 | String  | Yes      | The name of the course.
`class_id`             | String  | Yes      | The class's unique ID the course is based on.
`external_id`          | String  | No       | The user provided external ID of the course.
`days_limit`           | Number  | Yes      | The number of the days each enrollment will be limited to.
`activity_hours_limit` | Number  | Yes      | The number of work hours each enrollment will be limited to.
`status`               | String  | Yes      | The status of the course (`online`, `offline`).



## Delete a course

> Request Example

```shell
$ curl -X DELETE \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "http://app.strigo.io/api/v1/ondemand/i7gHDXnDzpRFQqFZP"
```

> Response Example

```json
{
  "result": "success"
}
```

### Usage

Delete a single course.

<aside class="notice">
You can only delete courses for which there are no running enrollments.
</aside>

`DELETE "/ondemand/:course_id"`

### URL Parameters

Attribute   | Type    | Required | Description
---------   | ------- | -------  | -------
`course_id` | String  | Yes      | The course's unique identifier.

