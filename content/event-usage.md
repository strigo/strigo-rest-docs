---
weight: 112
---


# Event Usage

Represents the current state of a **live** event.

## The Event Usage Resource

### Attributes:

Attribute               | Type     | Description
---------               | -------  | -------
`id`                    | String   | The usage object's unique identifier.
`event_id`              | String   | The event's unique identifier.
`usage`                 | Object   | An object containing the usage information.


## Retrieve a single workspace

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events/K6inELDjusK76rwGw/usage"
```

> Response Example

```json
{
        "id": "wN77kjAw6c46twt7A",
        "event_id": "K6inELDjusK76rwGw",
        "usage": {
            "attendees": {
                "hosts": 1,
                "tas": 2,
                "students": 79
            },
            "focused": 73,
            "active": 68,
            "following": 19
        }
    }

```

### Usage

Get usage for an event.

`GET "/events/:event_id/usage"`

### URL Parameters

Attribute      | Type    | Required | Description
---------      | ------- | -------  | -------
`event_id`     | String  | Yes      | The event's unique identifier.
