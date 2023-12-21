---
weight: 170
---

# Organization Partners

## The Partner Resource

### Attributes:

| Attribute | Type   | Description                                                |
|-----------|--------|------------------------------------------------------------|
| `id`      | String | The partner's unique identifier.                           |
| `name`    | String | The name of the partner as set by the parent organization. |

## Retrieve all partners

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/partners"
```

> Response Example

```json
{
  "data": [
    {
      "id": "yCoaiix2pRjxMjCn7",
      "name": "w00t"
    },
    {
      "id": "x6GHbXKBTPeAHpjmS",
      "name": "w00t1"
    },
    {
      "id": "hMJrmcqPDDjKwLN7Z",
      "name": "woot13"
    },
    {
      "id": "cYCk2Yq45qMQXGZkh",
      "name": "w00t3"
    },
    {
      "id": "ozSjhvAr8hMaQCLND",
      "name": "newa"
    },
    {
      "id": "mYsEBS6PeBeMpFCfQ",
      "name": "BLUASD"
    },
    {
      "id": "ggKqkNgY4KzQQoFsM",
      "name": "w00tasd"
    },
    {
      "id": "ntvXb3L2qdPbayRKZ",
      "name": "nur"
    }
  ],
  "result": "success"
}

```

### Usage

Lists all partners for your organization.

`GET "/partners"`

## Retrieve a single partner

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/ntvXb3L2qdPbayRKZ/ntvXb3L2qdPbayRKZ"
```

> Response Example

```json
{
  "data": {
    "id": "ntvXb3L2qdPbayRKZ",
    "name": "nur"
  },
  "result": "success"
}
```

### Usage

Get a single partner.

`GET "/partners/:partner_id"`

### URL Parameters

| Attribute    | Type   | Required | Description                      |
|--------------|--------|----------|----------------------------------|
| `partner_id` | String | Yes      | The partner's unique identifier. |

## Create a partner

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/partners" \
    -d @- <<EOF
    {
      "name":"My New Partner"
    }
EOF
```

> Response Example

```json
{
  "data": {
    "id": "Z3XKk7Swzr3MuaTGJ",
    "name": "My New Parnter"
  },
  "result": "success"
}
```

### Usage

Create a new partner.

`POST "/partners"`

### BODY Parameters

| Attribute | Type   | Required | Description              |
|-----------|--------|----------|--------------------------|
| `name`    | String | Yes      | The name of the partner. |

## Modify a partner

> Request Example

```shell
$ curl -X PATCH \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/partner/Z3XKk7Swzr3MuaTGJ" \
    -d @- <<EOF
    {
      "name":"New name for partner"
    }
EOF
```

> Response Example

```json
{
  "data": {
    "id": "Z3XKk7Swzr3MuaTGJ",
    "name": "New name for partner"
  },
  "result": "success"
}
```

### Usage

Modify a partner.

`PATCH "/partners/:partner_id"`

### URL Parameters

| Attribute    | Type   | Required | Description                      |
|--------------|--------|----------|----------------------------------|
| `partner_id` | String | Yes      | The partner's unique identifier. |

### BODY Parameters

| Attribute | Type   | Required | Description             |
|-----------|--------|----------|-------------------------|
| `name`    | String | Yes      | The partner's new name. |

## Retrieve partner members

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/partners/Z3XKk7Swzr3MuaTGJ/members"
```

> Response Example

```json
{
  "data": [
    {
      "email": "niro@strigo.io",
      "id": "MzkRF9fPnq34SatJB",
      "partner_id": "yCoaiix2pRjxMjCn7",
      "role": "partner"
    },
    {
      "email": "nira@strigo.io",
      "id": "BSwKLejmQtSsEyzE9",
      "partner_id": "yCoaiix2pRjxMjCn7",
      "role": "partner"
    }
  ],
  "result": "success"
}
```

### Usage

Retrieve parter members.

`GET "/partners/:partner_id/members"`

### URL Parameters

| Attribute    | Type   | Required | Description                      |
|--------------|--------|----------|----------------------------------|
| `partner_id` | String | Yes      | The partner's unique identifier. |

## Invite a partner member

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/partners/Z3XKk7Swzr3MuaTGJ/members" \
    -d @- <<EOF
    {
      "email":"trainer@partner-company.com"
    }
EOF
```

> Response Example

```json
{
  "data": {
    "created_at": "2019-01-07T15:42:21.932Z",
    "email": "trainer@partner-company.com",
    "id": "8unc2Gt4sGcqJgBqX",
    "link": "https://app.strigo.io/team/invite/LKOONmxKR2XcsbgKaz79xVVkAaPQyQ8PrX_1fVv3qFp",
    "partner_id": "Z3XKk7Swzr3MuaTGJ",
    "status": "pending"
  },
  "result": "success"
}
```

### Usage

Invite someone to join as a member in your defined partner entity.

`POST "/partners/:partner_id/members"`

### URL Parameters

| Attribute    | Type   | Required | Description                      |
|--------------|--------|----------|----------------------------------|
| `partner_id` | String | Yes      | The partner's unique identifier. |

### BODY Parameters

| Attribute | Type   | Required | Description                         |
|-----------|--------|----------|-------------------------------------|
| `email`   | String | Yes      | Email of partner trainer to invite. |

