---
weight: 100
---


# Classes

## The Class Resource

### Attributes:

Attribute               | Type     | Description
---------               | -------  | -------
`id`                    | String   | The class's unique identifier.
`name`                  | String   | The class's name.
`owner`                 | String   | The email or unique ID of the org member who created the class. Note that this is currently automatically inferred from the request, and has not effect on functionality.
`description`           | String   | The class's description.
`resources`             | List     | The lab resources chosen for the class (see [resources](#resources.md).
`presentation_notes`    | List     | The presentation notes added to the class's presentation (see [presentation notes](#presentation-notes.md).
`presentation_filename` | String   | The name of the presentation file (see [presentations](#presentations.md).


## Retrieve all classes

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes"
```

> Response Example

```json
[
  {
    "id": "K6inELDjusK76rwGw",
    "name": "Intro to Docker",
    "owner": {
        "email": "me@strigo.io",
        "id": "rMWNrMT2PCySh2PGo"
    },
    "presentation_notes": [],
    "resources": [
      {
        "id": "32xuu5Ap8G93CWA6X",
        "image_id": "ami-614dcd0e",
        "image_user": "ubuntu",
        "instance_type": "t2.large",
        "is_custom_image": false,
        "name": "Docker Node 1",
        "type": "lab_instance"
      },
      {
        "id": "DcnEqgGiBuisXadqe",
        "image_id": "ami-12312321",
        "image_user": "boot",
        "instance_type": "t2.medium",
        "is_custom_image": true,
        "name": "Docker Node 2",
        "type": "lab_instance"
      }
    ]
  }
]
```

### Usage

Lists all classes for your organization.

`GET "/classes"`


## Retrieve a single class

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/p3bdnrweEystFToCq"
```

> Response Example

```json
  {
    "id": "K6inELDjusK76rwGw",
    "name": "Intro to Docker",
    "owner": {
        "email": "me@strigo.io",
        "id": "rMWNrMT2PCySh2PGo"
    },
    "presentation_notes": [],
    "resources": [
      {
        "id": "32xuu5Ap8G93CWA6X",
        "image_id": "ami-614dcd0e",
        "image_user": "ubuntu",
        "instance_type": "t2.large",
        "is_custom_image": false,
        "name": "Docker Node 1",
        "type": "lab_instance"
      },
      {
        "id": "DcnEqgGiBuisXadqe",
        "image_id": "ami-12312321",
        "image_user": "boot",
        "instance_type": "t2.medium",
        "is_custom_image": true,
        "name": "Docker Node 2",
        "type": "lab_instance"
      }
    ]
  }
```

### Usage

Get a single class.

`GET "/classes/:class_id"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`class_id` | String  | Yes      | The class's unique identifier.


## Create a class

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes" \
    -d @- <<EOF
    {
      "name":"Intro to Docker"
    }
EOF
```

> Response Example

```json
{
  "id": "K6inELDjusK76rwGw",
  "name": "Intro to Docker",
  "owner": {
      "email": "me@strigo.io",
      "id": "rMWNrMT2PCySh2PGo"
  },
  "presentation_notes": [],
  "resources": []
}
```

### Usage

Create a new class.

`POST "/classes"`

### BODY Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`name`        | String   | Yes | The class's name.
`description` | String   | No  | The class's description.


## Modify a class

> Request Example

```shell
$ curl -X PATCH \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes" \
    -d @- <<EOF
    {
      "name":"Intro to Docker",
      "description": "Learning how to run and use Docker"
    }
EOF
```

> Response Example

```json
{
  "id": "K6inELDjusK76rwGw",
  "name": "Intro to Docker",
  "description": "Learning how to run and use Docker",
  "owner": {
      "email": "me@strigo.io",
      "id": "rMWNrMT2PCySh2PGo"
  },
  "presentation_notes": [],
  "resources": []
}
```

### Usage

Modify a class.

`PATCH "/classes/:class_id"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`class_id` | String  | Yes      | The class's unique identifier.

### BODY Parameters

Attribute     | Type     | Required | Description
---------     | -------  | -------  | -------
`name`        | String   | No       | The class's name.
`description` | String   | No       | The class's description.


## Delete a single class

> Request Example

```shell
$ curl -X DELETE \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/K6inELDjusK76rwGw"
```

> Response Example

```json
{
  "result": "success"
}
```

### Usage

Delete a single class.

`DELETE "/classes/:class_id"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`class_id` | String  | Yes      | The class's unique identifier.
