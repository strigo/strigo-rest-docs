---
weight: 130
---

# On Demand Courses

## The On Demand Course Resource

### Attributes:

| Attribute                   | Type    | Description                                                  |
|-----------------------------|---------|--------------------------------------------------------------|
| `id`                        | String  | The course's unique identifier.                              |
| `name`                      | String  | The name of the course.                                      |
| `course_link`               | String  | The course's attendance link.                                |
| `class_id`                  | String  | The class's unique ID the course is based on.                |
| `external_id`               | String  | The user provided external ID of the course.                 |
| `duration`                  | Number  | The time each enrollment will be available once started.     |
| `duration_unit`              | String  | The duration unit, either 'days' or 'hours'.                 |
| `activity_hours_limit`      | Number  | The number of work hours each enrollment will be limited to. |
| `features.video`            | Boolean | The flag for including video in the course.                  |
| `features.slides`           | Boolean | The flag for including slides in the course.                 |
| `features.lab_manual_pause` | Boolean | The flag for hiding workspace pause button.                  |
| `status`                    | String  | The status of the course (`online`, `offline`).              |
| `labels`                    | List    | The list of labels applied to the course.                    |

## Retrieve all courses

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand"
```

> Response Example

```json
[
  {
    "activity_hours_limit": 10,
    "class_id": "hd3ALTaLAbhfzmBbf",
    "course_link": "https://app.strigo.io/training/ondemand/nE5pDWGzFRRQ8uMrN",
    "duration": 5,
    "duration_unit": "days",
    "external_id": "course1",
    "id": "nE5pDWGzFRRQ8uMrN",
    "name": "Elastic Stack for beginners",
    "status": "online",
    "features": {
      "video": true,
      "slides": true,
      "lab_manual_pause": true
    }
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
    "https://app.strigo.io/api/v1/ondemand/nE5pDWGzFRRQ8uMrN"
```

> Response Example

```json
{
  "activity_hours_limit": 10,
  "class_id": "hd3ALTaLAbhfzmBbf",
  "course_link": "https://app.strigo.io/training/ondemand/nE5pDWGzFRRQ8uMrN",
  "duration": 5,
  "duration_unit": "days",
  "external_id": "course1",
  "id": "nE5pDWGzFRRQ8uMrN",
  "name": "Elastic Stack for beginners",
  "status": "online",
  "features": {
    "video": true,
    "slides": true,
    "lab_manual_pause": true
  }
}
```

### Usage

Get a single on demand course.

`GET "/ondemand/:course_id"`

### URL Parameters

| Attribute   | Type   | Required | Description                     |
|-------------|--------|----------|---------------------------------|
| `course_id` | String | Yes      | The course's unique identifier. |

## Create a course

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand" \
    -d @- <<EOF
      "name":"My Event",
      "class_id": "hd3ALTaLAbhfzmBbf",
      "duration": 5,
      "duration_unit": "days",
      "activity_hours_limit": 10,
      "status": "online",
      "external_id": "course1",
      "features": {
        "video": true,
        "slides": true,
        "lab_manual_pause": true
      }
    }
EOF
```

> Response Example

```json
{
  "activity_hours_limit": 10,
  "class_id": "hd3ALTaLAbhfzmBbf",
  "course_link": "https://app.strigo.io/training/ondemand/i7gHDXnDzpRFQqFZP",
  "duration": 5,
  "duration_unit": "days",
  "external_id": "course1",
  "id": "i7gHDXnDzpRFQqFZP",
  "name": "ooo",
  "status": "online",
  "features": {
    "video": true,
    "slides": true,
    "lab_manual_pause": true
  }
}
```

### Usage

Create a new on demand course.

`POST "/ondemand"`

### BODY Parameters

| Attribute                   | Type    | Required | Description                                                  |
|-----------------------------|---------|----------|--------------------------------------------------------------|
| `name`                      | String  | Yes      | The name of the course.                                      |
| `class_id`                  | String  | Yes      | The class's unique ID the course is based on.                |
| `external_id`               | String  | No       | The user provided external ID of the course.                 |
| `duration`                  | Number  | Yes      | The time each enrollment will be available once started.     |
| `duration_unit`              | Number  | Yes      | The duration unit, either 'days' or 'hours'.                 |
| `activity_hours_limit`      | Number  | Yes      | The number of work hours each enrollment will be limited to. |
| `features.video`            | Boolean | Yes      | The flag for including video in the course.                  |
| `features.slides`           | Boolean | Yes      | The flag for including slides in the course.                 |
| `features.lab_manual_pause` | Boolean | Yes      | The flag for hiding workspace pause button.                  |
| `status`                    | String  | Yes      | The status of the course (`online`, `offline`).              |
| `labels`                    | List    | No       | The list of labels to apply to the course.                   |

## Update a course

> Request Example

```shell
$ curl -X PATCH \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand/i7gHDXnDzpRFQqFZP" \
    -d @- <<EOF
      "name":"My Event",
      "class_id": "hd3ALTaLAbhfzmBbf",
      "duration": 5,
      "duration_unit": "days",
      "activity_hours_limit": 10,
      "status": "online",
      "external_id": "course1",
      "features": {
        "video": true,
        "slides": true,
        "lab_manual_pause": true
      }
    }
EOF
```

> Response Example

```json
{
  "activity_hours_limit": 10,
  "class_id": "hd3ALTaLAbhfzmBbf",
  "course_link": "https://app.strigo.io/training/ondemand/i7gHDXnDzpRFQqFZP",
  "duration": 5,
  "duration_unit": "days",
  "external_id": "course1",
  "id": "i7gHDXnDzpRFQqFZP",
  "name": "ooo",
  "status": "online",
  "features": {
    "video": true,
    "slides": true,
    "lab_manual_pause": true
  }
}
```

### Usage

Update an on demand course.

`PATCH "/ondemand/:ondemand_id"`

### BODY Parameters

| Attribute                   | Type    | Required | Description                                                  |
|-----------------------------|---------|----------|--------------------------------------------------------------|
| `name`                      | String  | No       | The name of the course.                                      |
| `class_id`                  | String  | No       | The class's unique ID the course is based on.                |
| `external_id`               | String  | No       | The user provided external ID of the course.                 |
| `duration`                  | Number  | No       | The time each enrollment will be available once started.     |
| `duration_unit`              | Number  | No       | The duration unit, either 'days' or 'hours'.                 |
| `activity_hours_limit`      | Number  | No       | The number of work hours each enrollment will be limited to. |
| `features.video`            | Boolean | No       | The flag for including video in the course.                  |
| `features.slides`           | Boolean | No       | The flag for including slides in the course.                 |
| `features.lab_manual_pause` | Boolean | No       | The flag for hiding workspace pause button.                  |
| `status`                    | String  | No       | The status of the course (`online`, `offline`).              |
| `labels`                    | List    | No       | The list of labels to apply to the course.                   |

## Delete a course

> Request Example

```shell
$ curl -X DELETE \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ondemand/i7gHDXnDzpRFQqFZP"
```

> Response Example

```text
204 No Content
```

### Usage

Delete a single course.

<aside class="notice">
You can only delete courses for which there are no running enrollments.
</aside>

`DELETE "/ondemand/:course_id"`

### URL Parameters

| Attribute   | Type   | Required | Description                     |
|-------------|--------|----------|---------------------------------|
| `course_id` | String | Yes      | The course's unique identifier. |
