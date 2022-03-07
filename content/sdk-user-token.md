---
weight: 910
---

# SDK User token

Before calling the [setup method in the SDK](https://github.com/strigo/strigo-sdk#setup), you need to generate a user token to identify the SDK user

## The User Token Resource

### Attributes:

| Attribute        | Type   | Description                                                                                 |
| ---------------- | ------ | ------------------------------------------------------------------------------------------- |
| `email`          | String | The user's unique email.                                                                    |
| `name`           | String | The name of the user.                                                                       |
| `externalUserId` | String | The user's identifier in your system.                                                       |
| `expiration`     | Number | Expiration date for the token - can be up to 2 months after the token creation (UNIX time). |

## Create a user token

Create a new user token.

`POST "/academy/users/token"`

### BODY Parameters

| Attribute        | Type   | Required | Default  | Description                                                                                 |
| ---------------- | ------ | -------- | -------- | ------------------------------------------------------------------------------------------- |
| `email`          | String | Yes      |          | The user's unique email.                                                                    |
| `name`           | String | No       | `""`     | The name of the user.                                                                       |
| `externalUserId` | String | No       | `""`     | The user's identifier in your system.                                                       |
| `expiration`     | Number | No       | 2 months | Expiration date for the token - can be up to 2 months after the token creation (UNIX time). |

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/academy/users/token" \
    -d @- <<EOF
    {
      email: "user1@strigo.io",
      name: "user1",
      externalUserId: "external-user-id",
      expiration: Date.now() + 2592000000,
    }
EOF
```

> Response Example

```json
{
  "result": "success",
  "data": {
    "user_id": "X7TnEwMSg66pBi8GZ",
    "expiration": 1648100582468,
    "token": "HfT31jk4WLIJ4f4ebR2MGzBIK0jp1M3tlbdvP20TBGd"
  }
}
```
