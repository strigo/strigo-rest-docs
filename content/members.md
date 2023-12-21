---
weight: 160
---

# Members

## The Member Resource

### Attributes:

| Attribute | Type   | Description                     |
|-----------|--------|---------------------------------|
| `id`      | String | The member's unique identifier. |
| `email`   | String | The member's email.             |
| `level`   | String | The member's role.              |

## Retrieve all members

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/members"
```

> Response Example

```json
[
  {
    "email": "me@strigo.io",
    "id": "rMWNrMT2PCySh2PGo",
    "role": "owner"
  },
  {
    "email": "me2@strigo.io",
    "id": "AsEM3RtnbuudJBZD5",
    "role": "member"
  }
]
```

### Usage

Lists all members for your organization.

`GET "/members"`
