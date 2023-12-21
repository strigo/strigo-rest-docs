---
weight: 115
---

# Event Workspaces

Workspaces are the technical entities which represent learners in an event.

A workspace contains some information about learner activities and state.

## The Workspace Resource

### Attributes:

| Attribute         | Type     | Description                                                            |
|-------------------|----------|------------------------------------------------------------------------|
| `id`              | String   | The workspace's unique identifier.                                     |
| `event_id`        | String   | The event id the workspace belongs to.                                 |
| `created_at`      | Datetime | The time when the workspace was created (attendee attended the event). |
| `type`            | String   | The type of the workspace (`host`, `ta`, `learner`).                   |
| `owner`           | Object   | The `email` and `id` of the org member hosting the event.              |
| `viewstate`       | String   | The position in the classroom the attendee is currently in.            |
| `online_status`   | String   | Whether the attendee is currently considered active or not.            |
| `last_seen`       | Datetime | The time when the user was last seen active.                           |
| `need_assistance` | Boolean  | Whether the workspace is currently asking for assistance.              |

## Retrieve all workspaces

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events/K6inELDjusK76rwGw/workspaces"
```

> Response Example

```json
[
  {
    "created_at": "2018-09-20T10:38:18.656Z",
    "id": "ECANkhaMraTFjFBSk",
    "last_seen": "2018-09-20T10:40:11.013Z",
    "need_assistance": false,
    "online_status": "online",
    "owner": {
      "email": "me@strigo.io",
      "id": "rMWNrMT2PCySh2PGo"
    },
    "type": "host"
  }
]
```

### Usage

Lists all workspaces for an event.

`GET "/events/:event_id/workspaces"`

## Retrieve a single workspace

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events/K6inELDjusK76rwGw/workspaces/ECANkhaMraTFjFBSk"
```

> Response Example

```json
{
  "created_at": "2018-09-20T10:38:18.656Z",
  "id": "ECANkhaMraTFjFBSk",
  "last_seen": "2018-09-20T10:40:11.013Z",
  "need_assistance": false,
  "online_status": "online",
  "owner": {
    "email": "me@strigo.io",
    "id": "rMWNrMT2PCySh2PGo"
  },
  "type": "host"
}
```

### Usage

Get a single workspace.

`GET "/events/:event_id/workspaces/:workspace_id"`

### URL Parameters

| Attribute      | Type   | Required | Description                        |
|----------------|--------|----------|------------------------------------|
| `event_id`     | String | Yes      | The event's unique identifier.     |
| `workspace_id` | String | Yes      | The workspace's unique identifier. |

