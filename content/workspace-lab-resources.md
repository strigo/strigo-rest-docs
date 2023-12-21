---
weight: 115
---

# Workspace Lab Resources

A workspace lab resource is a reference to the actual lab created for a workspace.

## The Workspace Lab Resource

### Attributes:

| Attribute         | Type   | Description                                                           |
|-------------------|--------|-----------------------------------------------------------------------|
| `id`              | String | The resource's unique identifier.                                     |
| `event_id`        | String | The event id the resource belongs to.                                 |
| `type`            | String | The type of the resource.                                             |
| `public_ip`       | String | The publically accessible IP of the resource.                         |
| `private_ip`      | String | The private IP of the resource (accessible from other lab resources). |
| `workspace_id`    | String | The id of the workspace the resource belongs to.                      |
| `connection_type` | String | The type of interface this resource is accessed by (RDP/SSH).         |
| `host`            | String | The publically accessible host string of the resource.                |
| `port`            | String | The port through which which this resource can be accessed.           |
| `status`          | String | The status of the resource.                                           |
| `strigo_dns`      | String | The publically accessible DNS name of the resource.                   |

## Retrieve all workspace resources

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/events/K6inELDjusK76rwGw/workspaces/ECANkhaMraTFjFBSk/resources"
```

> Response Example

```json
[
  {
    "id": "asANksdMTqjegKTLM",
    "event_id": "K6inELDjusK76rwGw",
    "workspace_id": "ECANkhaMraTFjFBSk",
    "public_ip": "3.124.187.66",
    "private_ip": "172.31.23.29",
    "type": "lab_instance",
    "host": "ec2-3-124-187-66.eu-central-1.compute.amazonaws.com",
    "port": "22",
    "connection_type": "ssh",
    "status": "running",
    "strigo_dns": "ecankhamratfjfbsk-heflvgbrrknpdfi2y.labs.strigo.io"
  }
]
```

### Usage

Lists all resources for an workspace.

`GET "/events/:event_id/workspaces/:workspace_id/resources"`

### URL Parameters

| Attribute      | Type   | Required | Description                        |
|----------------|--------|----------|------------------------------------|
| `event_id`     | String | Yes      | The event's unique identifier.     |
| `workspace_id` | String | Yes      | The workspace's unique identifier. |
