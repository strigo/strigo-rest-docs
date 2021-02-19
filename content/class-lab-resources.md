---
weight: 103
---


# Class Lab Resources

## The Class Lab Resource

### Attributes:

Attribute               | Type     | Description
---------               | -------  | -------
`id`                    | String   | The resources's unique identifier.
`type`                  | String   | Currently `instance_type`.
`name`                  | String   | The resource's display name.
`image_id`              | String   | The instance's AMI ID.
`image_user`            | String   | The user with which to connect to the instance.
`is_custom_image`       | Boolean  | Whether the configured image is a custom one or a build-in one.
`webview_links`         | List     | A list of webview links.
`post_launch_script`    | String   | A multiline script to run after all instances in the workspace have loaded.
`userdata`              | String   | A multiline script to run after the intance loads.
`ec2_region`            | String   | The AWS region in which the instance is running.
`instance_type`         | String   | The type of the instance.


## Retrieve all lab resources

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/K6inELDjusK76rwGw/resources"
```

> Response Example

```json
[
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
```

### Usage

Lists all lab resources for a class.

`GET "/classes/:class_id/resources"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`class_id` | String  | Yes      | The class's unique identifier.


## Retrieve a single lab resource

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/K6inELDjusK76rwGw/resources/DcnEqgGiBuisXadqe"
```

> Response Example

```json
{
  "id": "DcnEqgGiBuisXadqe",
  "image_id": "ami-12312321",
  "image_user": "boot",
  "instance_type": "t2.medium",
  "is_custom_image": true,
  "name": "Docker Node 2",
  "type": "lab_instance"
}
```

### Usage

Get a single lab resource.

`GET "/classes/:class_id/resources/:resource_id"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`class_id` | String  | Yes      | The class's unique identifier.
`resource_id` | String | Yes    | The resource's unique identifier.


## Create a lab resource

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/K6inELDjusK76rwGw/resources" \
    -d @- <<EOF
    {
      "image_id":"ami-0ea21e760f354e854",
      "image_user": "ubuntu",
      "name": "My Lab",
      "webview_links": [{"url": "http://instance.autolab.strigo.io", "name":"My Lab Link"}]
    }
EOF
```

> Response Example

```json
{
  "type": "lab_instance",
  "id": "4mh5E8HwFYzeYSMAD",
  "name": "My Lab",
  "instance_type": "t2.medium",
  "image_id": "ami-0ea21e760f354e854",
  "image_user": "ubuntu",
  "is_custom_image": true,
  "webview_links": [
    {
        "name": "My Lab Link",
        "url": "://instance.autolab.strigo.io"
    }
  ]
}
```

### Usage

Create a new lab resource.

`PATCH "/classes/:class_id/resources"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`class_id` | String  | Yes      | The class's unique identifier.

### BODY Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`name`               | String | Yes | The resource's display name.
`image_id`           | String | Yes | The instance's AMI ID.
`image_user`         | String | Yes | The user with which to connect to the instance.
`webview_links`      | List   | No  | A list of webview links.
`post_launch_script` | String | No  | A multiline script to run after all instances in the workspace have loaded.
`userdata`           | String | No  | A multiline script to run after the intance loads.
`ec2_region`         | String | No  | The AWS region in which the instance is running (default: `eu-central-1`).
`instance_type`      | String | No  | The type of the instance available for your org (default: `t2.medium`).

### WEBVIEW LINK Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`name`     | String | Yes | The display name for the link.
`url`      | String | Yes | The url to use.


## Modify a lab resource

> Request Example

```shell
$ curl -X PATCH \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/K6inELDjusK76rwGw/resources/DcnEqgGiBuisXadqe" \
    -d @- <<EOF
    {
      "image_id":"ami-1111111111",
      "image_user": "ubuntu",
      "name": "My Lab 2",
      "webview_links": [{"url": "http://instance.autolab.strigo.io", "name":"My Lab Link"}]
    }
EOF
```

> Response Example

```json
{
  "type": "lab_instance",
  "id": "4mh5E8HwFYzeYSMAD",
  "name": "My Lab 2",
  "instance_type": "t2.medium",
  "image_id": "ami-0ea21e760f354e854",
  "image_user": "ubuntu",
  "is_custom_image": true,
  "webview_links": [
    {
        "name": "My Lab Link",
        "url": "://instance.autolab.strigo.io"
    }
  ]
}
```

### Usage

Modify a lab resource.

`POST "/classes/:class_id/resources/:resource_id"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`class_id` | String  | Yes      | The class's unique identifier.
`resource_id` | String | Yes    | The resource's unique identifier.

### BODY Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`name`               | String | No  | The resource's display name.
`image_id`           | String | No  | The instance's AMI ID.
`image_user`         | String | No  | The user with which to connect to the instance.
`webview_links`      | List   | No  | A list of webview links.
`post_launch_script` | String | No  | A multiline script to run after all instances in the workspace have loaded.
`userdata`           | String | No  | A multiline script to run after the intance loads.
`ec2_region`         | String | No  | The AWS region in which the instance is running (default: `eu-central-1`).
`instance_type`      | String | No  | The type of the instance available for your org (default: `t2.medium`).

### WEBVIEW LINK Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`name`     | String | Yes | The display name for the link.
`url`      | String | Yes | The url to use.


## Delete a single lab resource

> Request Example

```shell
$ curl -X DELETE \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/K6inELDjusK76rwGw/resources/DcnEqgGiBuisXadqe"
```

> Response Example

```text
204 No Content
```


### Usage

Delete a single lab resource.

`DELETE "/classes/:class_id/resources/:resource_id"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`class_id` | String  | Yes      | The class's unique identifier.
`resource_id` | String | Yes    | The resource's unique identifier.
