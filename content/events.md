---
weight: 110
---

# Events

## The Event Resource

### Attributes:

Attribute           | Type     | Description
---------           | -------  | -------
`id`                | String   | The event's unique identifier.
`owner`             | Object   | The `email` and `id` of the org member hosting the event.
`name`              | String   | The event's name.
`event_link`        | String   | The event's link.
`token`             | String   | The event's public access token.
`class_id`          | String   | The unique id of the class the event is based on.
`availability`      | String   | public/private
`description`       | String   | The event's description.
`date_start`        | Datetime | The date when the event starts (ISO8601).
`date_end`          | Datetime | The date when the event ends (ISO8601).
`include_chat`      | Boolean  | Whether the event should include chat.
`include_video`     | Boolean  | Whether the event should include video.
`tas`               | List     | A list of training assistant emails.
`trainees`          | List     | A list of student emails (for private only).
`status`            | String   | The status of the event.
`partner_id`        | String   | The unique ID of the partner entity to which this event belongs.
`use_new_terminal`  | Boolean  | Whether the event should use new terminal (beta). 


## Retrieve all events

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events"
```

> Response Example

```json
[
    {
        "availability": "public",
        "class_id": "hd3ALTaLAbhfzmBbf",
        "date_end": "2018-09-20T12:00:00.000Z",
        "date_start": "2018-09-20T11:00:00.000Z",
        "event_link": "https://app.strigo.io/event/p3bQnrweEystFToCq",
        "id": "p3bdnrweEystFToCq",
        "include_chat": false,
        "include_video": false,
        "name": "My Event",
        "owner": {
            "email": "me@strigo.io",
            "id": "rMWNrMT2pCySh2PGo"
        },
        "status": "live",
        "tas": [],
        "token": "9NX4",
        "trainees": [],
        "use_new_terminal": false
    }
]
```

### Usage

Lists all events for your organization, regardless of their status.

`GET "/events"`


## Retrieve a single event

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events/p3bdnrweEystFToCq"
```

> Response Example

```json
{
    "availability": "public",
    "class_id": "hd3ALTaLAbhfzmBbf",
    "date_end": "2018-09-20T12:00:00.000Z",
    "date_start": "2018-09-20T11:00:00.000Z",
    "event_link": "https://app.strigo.io/event/p3bQnrweEystFToCq",
    "id": "p3bdnrweEystFToCq",
    "include_chat": false,
    "include_video": false,
    "name": "My Event",
    "owner": {
        "email": "me@strigo.io",
        "id": "rMWNrMT2pCySh2PGo"
    },
    "status": "live",
    "tas": [],
    "token": "9NX4",
    "trainees": [],
    "use_new_terminal": false
}
```

### Usage

Get a single event.

`GET "/events/:event_id"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`event_id` | String  | Yes      | The event's unique identifier.


## Create an event

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events" \
    -d @- <<EOF
    {
      "name":"My Event",
      "date_end": "2018-10-30T13:00:00.000Z",
      "date_start": "2018-09-20T11:00:00.000Z",
      "owner": "me@strigo.io",
      "class_id": "hd3ALTaLAbhfzmBbf"
    }
EOF
```

> Response Example

```json
{
    "availability": "public",
    "class_id": "hd3ALTaLAbhfzmBbf",
    "date_end": "2018-10-30T13:00:00.000Z",
    "date_start": "2018-09-20T11:00:00.000Z",
    "event_link": "https://app.strigo.io/event/p3bQnrweEystFToCq",
    "id": "p3bdnrweEystFToCq",
    "include_chat": false,
    "include_video": false,
    "name": "My Event",
    "owner": {
        "email": "me@strigo.io",
        "id": "rMWNrMT2pCySh2PGo"
    },
    "status": "live",
    "tas": [],
    "token": "9NX4",
    "trainees": [],
    "use_new_terminal": false
}
```

### Usage

Create a new event.

`POST "/events"`

### BODY Parameters

Attribute           | Type     | Required | Description
---------           | -------  |  ------- | -------
`name`              | String   | Yes      | The event's name (limited to 256 chars).
`owner`             | String   | Yes      | The email of the org member hosting the event.
`class_id`          | String   | Yes      | The unique id of the class the event is based on.
`description`       | String   | No       | The event's description (limited to 65536 chars).
`date_start`        | Datetime | Yes      | The date when the event starts (ISO8601).
`date_end`          | Datetime | Yes      | The date when the event ends (ISO8601).
`include_chat`      | Boolean  | No       | Whether the event should include chat.
`include_video`     | Boolean  | No       | Whether the event should include video.
`tas`               | List     | No       | A list of training assistant emails.
`trainees`          | List     | No       | A list of student emails (adding trainees implicitly creates a private event).
`use_new_terminal`  | Boolean  | No       | Whether the event should use new terminal (beta). 

## Modify an event

> Request Example

```shell
$ curl -X PATCH \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events" \
    -d @- <<EOF
    {
        "name": "Another Event",
        "owner": "someone.else@strigo.io"
    }
EOF
```

> Response Example

```json
{
    "availability": "public",
    "class_id": "hd3ALTaLAbhfzmBbf",
    "date_end": "2018-10-30T13:00:00.000Z",
    "date_start": "2018-09-20T11:00:00.000Z",
    "event_link": "https://app.strigo.io/event/p3bQnrweEystFToCq",
    "id": "p3bdnrweEystFToCq",
    "include_chat": false,
    "include_video": false,
    "name": "Another Event",
    "owner": {
        "email": "someone.else@strigo.io",
        "id": "LLWdr8TFpRTS022Go"
    },
    "status": "live",
    "tas": [],
    "token": "9NX4",
    "trainees": [],
    "use_new_terminal": false
}
```

### Usage

Modify an existing event.

`PATCH "/events/:event_id"`

### URL Parameters

Attribute           | Type     | Required | Description
---------           | -------  | -------  | -------
`event_id`          | String   | Yes      | The event's unique identifier.

### BODY Parameters

Attribute           | Type     | Required | Description
---------           | -------  | -------  | -------
`name`              | String   | No       | The event's name (limited to 256 chars).
`owner`             | String   | No       | The email of the org member hosting the event.
`description`       | String   | No       | The event's description (limited to 65536 chars).
`date_start`        | Datetime | No       | The date when the event starts (ISO8601).
`date_end`          | Datetime | No       | The date when the event ends (ISO8601).
`class_id`          | String   | No       | The unique id of the class the event is based on.
`include_chat`      | Boolean  | No       | Whether the event should include chat.
`include_video`     | Boolean  | No       | Whether the event should include video.
`tas`               | List     | No       | A list of training assistant emails.
`trainees`          | List     | No       | A list of student emails (adding trainees implicitly means a private event).

<aside class="notice">
You cannot currently modify live events. That will be supported in the future.
</aside>




## Delete an event

> Request Example

```shell
$ curl -X DELETE \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events/p3bdnrweEystFToCq"
```

> Response Example

```json
{
  "result": "success"
}
```

### Usage

Delete a single event.

<aside class="notice">
You can only delete events in `ready` state.
</aside>

`DELETE "/events/:event_id"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`event_id` | String  | Yes      | The event's unique identifier.
