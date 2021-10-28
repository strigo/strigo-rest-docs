---
weight: 900
---

# Subscriptions

## The Subscription Resource

### Attributes:

Attribute               | Type     | Description
---------               | -------  | -------
`id`                    | String   | The event's unique identifier.
`target`                | String   | The URL to send the payload to.
`event`                 | String   | The type of event to send notifications to.
`status`                | String   | The status of the subscription (Can be either `active` or `inactive`).
`createdAt`             | Datetime | The date when the subscription was created (ISO8601).
`updatedAt`             | Datetime | The date when the subscription was updated (ISO8601).

#### Available event types:

See our [Subscriptions API help article](http://help.strigo.io/en/articles/5685041-using-strigo-s-subscriptions-api) for more info.


## Retrieve all subscriptions

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/subscriptions"
```

> Response Example

```json
{
  "result": "success",
  "data": [
    {
      "id": "dZXxzYYhgEGayy7Mc",
      "event": "enrollment.create",
      "target": "https://example.com",
      "status": "active",
      "createdAt": "2021-10-26T06:32:18.655Z",
      "updatedAt": "2021-10-26T06:32:18.655Z"
    },
    {
      "id": "WtYjHKG3qPfhbb3sx",
      "event": "event.create",
      "target": "https://example.com",
      "status": "active",
      "createdAt": "2021-10-26T17:59:08.109Z",
      "updatedAt": "2021-10-26T17:59:08.109Z"
    }
  ]
}
```

### Usage

Lists all subscriptions for your organization, regardless of their status.

`GET "/subscriptions"`


## Retrieve a single subscription

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/subscriptions/dZXxzYYhgEGayy7Mc"
```

> Response Example

```json
{
  "result": "success",
  "data": {
    "id": "dZXxzYYhgEGayy7Mc",
    "event": "enrollment.create",
    "target": "https://example.com",
    "status": "active",
    "createdAt": "2021-10-26T06:32:18.655Z",
    "updatedAt": "2021-10-26T06:32:18.655Z"
  }
}
```

### Usage

Get a single subscription.

`GET "/subscriptions/:subscription_id"`

### URL Parameters

Attribute         | Type    | Required | Description
---------         | ------- | -------  | -------
`subscription_id` | String  | Yes      | The subscription's unique identifier.


## Create an subscription

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/subscription" \
    -d @- <<EOF
    {
      "target":"https://example.com",
      "event": "partner.create"
    }
EOF
```

> Response Example

```json
{
  "result": "success",
  "data": {
    "id": "x6L3vCNXcvkJXYdd3",
    "event": "partner.create",
    "target": "https://example.com",
    "status": "active",
    "createdAt": "2021-10-28T09:57:14.354Z",
    "updatedAt": "2021-10-28T09:57:14.354Z"
  }
}
```

### Usage

Create a new subscription.

`POST "/subscriptions"`

### BODY Parameters

Attribute | Type     | Required | Description
--------- | -------  |  ------- | -------
`target`  | String   | Yes      | The target to send the notification to.
`event`   | String   | Yes      | The type of the event to subscribe to.
`status`  | String   | No       | The status of the subscription (Can be either `active` or `inactive`).

## Modify a subscription

> Request Example

```shell
$ curl -X PATCH \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/subscription" \
    -d @- <<EOF
    {
      "target":"https://example.com",
      "event": "partner.create",
      "status": "inactive"
    }
EOF
```

> Response Example

```json
{
  "result": "success",
  "data": {
    "id": "x6L3vCNXcvkJXYdd3",
    "event": "partner.create",
    "target": "https://example.com",
    "status": "inactive",
    "createdAt": "2021-10-28T09:57:14.354Z",
    "updatedAt": "2021-10-28T09:57:14.354Z"
  }
}
```

### Usage

Modify an existing subscription.

`PATCH "/subscriptions/:subscription_id"`

### URL Parameters

Attribute         | Type    | Required | Description
---------         | ------- | -------  | -------
`subscription_id` | String  | Yes      | The subscription's unique identifier.

### BODY Parameters

Attribute | Type     | Required | Description
--------- | -------  |  ------- | -------
`target`  | String   | Yes      | The target to send the notification to.
`event`   | String   | Yes      | The type of the event to subscribe to.
`status`  | String   | No       | The status of the subscription (Can be either `active` or `inactive`).


## Delete a subscription

> Request Example

```shell
$ curl -X DELETE \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/subscriptions/x6L3vCNXcvkJXYdd3"
```

> Response Example

```text
204 No Content
```


### Usage

Delete a single subscription.

`DELETE "/subscription/:subscription_id"`

### URL Parameters

Attribute         | Type    | Required | Description
---------         | ------- | -------  | -------
`subscription_id` | String  | Yes      | The subscription's unique identifier.
