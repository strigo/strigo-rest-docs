---
weight: 103
---

# Class Lab Resources

## The Class Lab Resource

### Attributes:

| Attribute              | Type    | Description                                                                 |
|------------------------|---------|-----------------------------------------------------------------------------|
| `id`                   | String  | The resources's unique identifier.                                          |
| `type`                 | String  | Currently `instance_type`.                                                  |
| `name`                 | String  | The resource's display name.                                                |
| `image_id`             | String  | The instance's AMI ID.                                                      |
| `image_user`           | String  | The user with which to connect to the instance.                             |
| `is_custom_image`      | Boolean | Whether the configured image is a custom one or a build-in one.             |
| `webview_links`        | List    | A list of webview links.                                                    |
| `post_launch_script`   | String  | A multiline script to run after all instances in the workspace have loaded. |
| `userdata`             | String  | A multiline script to run after the intance loads.                          |
| `ec2_region`           | String  | The AWS region in which the instance is running.                            |
| `instance_type`        | String  | The type of the instance.                                                   |
| `image_region_mapping` | Object  | A mapping of AWS regions to AMI IDs.                                        |

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

> Request Example with AMI region mapping

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/KsK766inELDjurwGw/resources"
```

> Response Example with AMI region mapping

```json
{
  "result": "success",
  "data": [
    {
      "type": "lab_instance",
      "id": "640d9bc7dcd2f2152Sxc82fd",
      "name": "centos",
      "instance_type": "t3.medium",
      "image_id": "ami-03aae0a64be2fab88",
      "image_user": "Admin",
      "image_region_mapping": {
        "us-east-1": "ami-03aae688d154e2fab88",
        "us-west-1": "ami-00f6e688d14e2fab885"
      },
      "is_custom_image": true,
      "webview_links": [],
      "ec2_region": "us-east-1",
      "view_interface": "terminal"
    },
    {
      "type": "lab_instance",
      "id": "uJQi9fku97WQLRo5",
      "name": "My Lab 12-02-24",
      "instance_type": "t3.medium",
      "image_user": "ubuntu",
      "image_region_mapping": {
        "eu-west-1": "ami-0e6463ab1952d9fc3"
      },
      "is_custom_image": true,
      "webview_links": [],
      "ec2_region": "eu-west-1",
      "view_interface": "terminal"
    },
    {
      "type": "lab_instance",
      "id": "3khf5ooi9fku97WQN",
      "name": "My global lab",
      "instance_type": "t3.medium",
      "image_user": "ubuntu",
      "image_region_mapping": {
        "eu-west-1": "ami-030ba4e58e4fabsa",
        "us-east-1": "ami-0cf5430f423ed73c14a7",
        "ap-northeast-1": "ami-c9c7cd833009a4079",
        "ap-southeast-1": "ami-6981eeb0fab165bfb"
      },
      "is_custom_image": true,
      "webview_links": [],
      "ec2_region": "eu-west-1",
      "view_interface": "terminal"
    }
  ]
}
```

### Usage

Lists all lab resources for a class.

`GET "/classes/:class_id/resources"`

### URL Parameters

| Attribute  | Type   | Required | Description                    |
|------------|--------|----------|--------------------------------|
| `class_id` | String | Yes      | The class's unique identifier. |

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

| Attribute     | Type   | Required | Description                       |
|---------------|--------|----------|-----------------------------------|
| `class_id`    | String | Yes      | The class's unique identifier.    |
| `resource_id` | String | Yes      | The resource's unique identifier. |

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


> Request Example with AMI region mapping

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/K6inELDjusK76rwGw/resources" \
    -d @- <<EOF
    {
      "image_user": "ubuntu",
      "name": "My Lab",
      "webview_links": [{"url": "http://instance.autolab.strigo.io", "name":"My Lab Link"}]
      "image_region_mapping": {"us-east-1": "ami-0ea214e760f354e85", "eu-west-1": "ami-a21e760f354e8540e"}
    }
EOF
```

> Response Example with AMI region mapping

```json
{
  "type": "lab_instance",
  "id": "4mh5E8HwFYzeYSMAD",
  "name": "My Lab",
  "instance_type": "t2.medium",
  "image_user": "ubuntu",
  "is_custom_image": true,
  "webview_links": [
    {
      "name": "My Lab Link",
      "url": "://instance.autolab.strigo.io"
    }
  ],
  "image_region_mapping": { 
    "us-east-1": "ami-0ea214e760f354e85", 
    "eu-west-1": "ami-a21e760f354e8540e"
  }
}
```

### Usage

Create a new lab resource.

`PATCH "/classes/:class_id/resources"`

### URL Parameters

| Attribute  | Type   | Required | Description                    |
|------------|--------|----------|--------------------------------|
| `class_id` | String | Yes      | The class's unique identifier. |

### BODY Parameters

| Attribute              | Type   | Required | Description                                                                 |
|------------------------|--------|----------|-----------------------------------------------------------------------------|
| `name`                 | String | Yes      | The resource's display name.                                                |
| `image_id`             | String | Yes      | The instance's AMI ID.                                                      |
| `image_user`           | String | Yes      | The user with which to connect to the instance.                             |
| `webview_links`        | List   | No       | A list of webview links.                                                    |
| `post_launch_script`   | String | No       | A multiline script to run after all instances in the workspace have loaded. |
| `userdata`             | String | No       | A multiline script to run after the intance loads.                          |
| `ec2_region`           | String | No       | The AWS region in which the instance is running (default: `eu-central-1`).  |
| `instance_type`        | String | No       | The type of the instance available for your org (default: `t2.medium`).     |
| `image_region_mapping` | Object | No       | A mapping of AWS regions to AMI IDs.                                        |

### WEBVIEW LINK Parameters

| Attribute | Type   | Required | Description                    |
|-----------|--------|----------|--------------------------------|
| `name`    | String | Yes      | The display name for the link. |
| `url`     | String | Yes      | The url to use.                |

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

> Request Example with AMI region mapping

```shell
$ curl -X PATCH \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/K6inELDjusK76rwGw/resources/DcnEqgGiBuisXadqe" \
    -d @- <<EOF
    {
      "image_user": "ubuntu",
      "name": "My Lab 2",
      "webview_links": [{"url": "http://instance.autolab.strigo.io", "name":"My Lab Link"}],
      "image_region_mapping": {"us-east-1": "ami-0ea214e760f354e85", "eu-west-1": "ami-a21e760f354e8540e"}
    }
EOF
```

> Response Example with AMI region mapping

```json
{
  "type": "lab_instance",
  "id": "4mh5E8HwFYzeYSMAD",
  "name": "My Lab 2",
  "instance_type": "t2.medium",
  "image_user": "ubuntu",
  "is_custom_image": true,
  "webview_links": [
    {
      "name": "My Lab Link",
      "url": "://instance.autolab.strigo.io"
    }
  ],
  "image_region_mapping": {
    "us-east-1": "ami-0ea214e760f354e85",
    "eu-west-1": "ami-a21e760f354e8540e"
  }
}
```

### Usage

Modify a lab resource.

`PATCH "/classes/:class_id/resources/:resource_id"`

### URL Parameters

| Attribute     | Type   | Required | Description                       |
|---------------|--------|----------|-----------------------------------|
| `class_id`    | String | Yes      | The class's unique identifier.    |
| `resource_id` | String | Yes      | The resource's unique identifier. |

### BODY Parameters

| Attribute            | Type   | Required | Description                                                                 |
|----------------------|--------|----------|-----------------------------------------------------------------------------|
| `name`               | String | No       | The resource's display name.                                                |
| `image_id`           | String | No       | The instance's AMI ID.                                                      |
| `image_user`         | String | No       | The user with which to connect to the instance.                             |
| `webview_links`      | List   | No       | A list of webview links.                                                    |
| `post_launch_script` | String | No       | A multiline script to run after all instances in the workspace have loaded. |
| `userdata`           | String | No       | A multiline script to run after the intance loads.                          |
| `ec2_region`         | String | No       | The AWS region in which the instance is running (default: `eu-central-1`).  |
| `instance_type`      | String | No       | The type of the instance available for your org (default: `t2.medium`).     |

### WEBVIEW LINK Parameters

| Attribute | Type   | Required | Description                    |
|-----------|--------|----------|--------------------------------|
| `name`    | String | Yes      | The display name for the link. |
| `url`     | String | Yes      | The url to use.                |

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

| Attribute     | Type   | Required | Description                       |
|---------------|--------|----------|-----------------------------------|
| `class_id`    | String | Yes      | The class's unique identifier.    |
| `resource_id` | String | Yes      | The resource's unique identifier. |
