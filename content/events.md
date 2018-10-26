---
weight: 110
---

# Events

## The Event Resource

### Attributes:

Attribute | Type | Description
--------- | ------- | -------
`id` | String | The event's unique identifier.
`owner` | String | The email or unique ID of the org member hosting the event.
`name` | String | The event's name.
`event_link` | String | The event's link.
`token` | String | The event's public access token.
`class_id` | String | The unique id of the class the event is based on.
`availability` | String | public/private
`description` | String | The event's description.
`date_start` | Datetime | The date when the event starts.
`date_end` | Datetime | The date when the event ends.
`include_chat` | Boolean | Whether the event should include chat.
`include_video` | Boolean | Whether the event should include video.
`tas` | List | A list of training assistant emails.
`trainees` | List | A list of student emails (for private only).
`use_new_console` | Boolean | Whether to use the new console or not (Beta).
`status` | String | The status of the event.

## Retrieve all events

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "http://app.strigo.io/api/v1/events"
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
        "use_new_console": false
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
    "http://app.strigo.io/api/v1/events/p3bdnrweEystFToCq"
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
    "use_new_console": false
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
    "http://app.strigo.io/api/v1/events" \
    -d { \
      "name":"My Event", \
      "date_end": "2018-10-30T13:00:00.000Z", \
      "date_start": "2018-09-20T11:00:00.000Z", \
      "owner": "me@strigo.io", \
      "class_id": "hd3ALTaLAbhfzmBbf" \
    }
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
    "use_new_console": false
}
```

### Usage

Create a new event.

`POST "/events"`

### BODY Parameters

Attribute           | Type     | Required | Description
---------           | -------  |  ------- | -------
`name`              | String   | Yes      | The event's name.
`owner`             | String   | Yes      | The email or unique ID of the org member hosting the event.
`class_id`          | String   | Yes      | The unique id of the class the event is based on.
`description`       | String   | No       | The event's description.
`date_start`        | Datetime | Yes      | The date when the event starts.
`date_end`          | Datetime | Yes      | The date when the event ends.
`include_chat`      | Boolean  | No       | Whether the event should include chat.
`include_video`     | Boolean  | No       | Whether the event should include video.
`tas`               | List     | No       | A list of training assistant emails.
`trainees`          | List     | No       | A list of student emails (adding trainees implicitly creates a private event).
`use_new_console`   | Boolean  | No       | Whether to use the new console or not (Beta).


## Modify an event

> Request Example

```shell
$ curl -X PATCH \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "http://app.strigo.io/api/v1/events" \
    -d {"name":"Someone Else's Event", "owner": "someone.else@strigo.io"}
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
    "name": "Someone Else's Event",
    "owner": {
        "email": "someone.else@strigo.io",
        "id": "LLWdr8TFpRTS022Go"
    },
    "status": "live",
    "tas": [],
    "token": "9NX4",
    "trainees": [],
    "use_new_console": false
}
```

### Usage

Create a new event.

`PATCH "/events/:event_id"`

### URL Parameters

Attribute           | Type     | Required | Description
---------           | -------  | -------  | -------
`event_id`          | String   | Yes      | The event's unique identifier.

### BODY Parameters

Attribute           | Type     | Required | Description
---------           | -------  | -------  | -------
`name`              | String   | No       | The event's name.
`owner`             | String   | No       | The email or unique ID of the org member hosting the event.
`description`       | String   | No       | The event's description.
`date_start`        | Datetime | No       | The date when the event starts (only for events that haven't started).
`date_end`          | Datetime | No       | The date when the event ends (only for events that haven't started).
`tas`               | List     | No       | A list of training assistant emails (only for events that haven't started).

We will be gradually adding additional functionality for changing event student list, and more.



## Delete an event

> Request Example

```shell
$ curl -X DELETE \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "http://app.strigo.io/api/v1/events/p3bdnrweEystFToCq"
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

