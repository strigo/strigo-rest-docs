---
weight: 1010
---


# Webhooks - Incoming Messages

## Incoming Message

The following messages are sent from the customer's backend to Strigo, where Strigo can then perform any required actions.

For example, once the customer's backend has created a lab for a student, Strigo can use the information from the incoming message to display a terminal interface.

See [Outgoing Messages](#webhooks-outgoing-messages) for examples on the webhook messages Strigo sends.

### Incoming message attributes:

Attribute               | Type     | Description
---------               | -------  | -------
`source_message_id`     | String   | The source message's unique identifier. This is the `message_id` as provided in the outgoing message.
`type`                  | String   | The type of resource Strigo needs to handle.
`action`                | String   | The performed action.
`data`                  | Object   | An object containing `resources` and `interfaces` lists.
`timestamp`             | Datetime | An ISO8601 compatible timestamp.

#### Resource attributes:

Attribute               | Type     | Description
---------               | -------  | -------
`id`                    | String   | The resource's unique identifier. This is defined by the customer, and can be refernced later in a Strigo interface.
`type`                  | String   | The type of resource Strigo needs to handle.
`status`                | String   | The current status of the resource. See [list of possible resource statuses](#resource-statuses) below.
`name`                  | String   | The name of the resource. This will be used for auditing purposes.
`config`                | Object   | Any mandatory or optional configuration for the resource.

#### Interface attributes:

Attribute               | Type     | Description
---------               | -------  | -------
`name`                  | String   | A name for the interface, which will be displayed for the attendees.
`type`                  | String   | The type of interace to be used to connect to the resource.
`region`                | String   | The location from which Strigo will attempt to connect to the referenced resource. This affects latency for the different interfaces. See [available regions](#available-regions) for a list of available regions.
`resource_id`           | String   | The resource's unique identifier, as defined in the `resource` object.
`config`                | Object   | Any mandatory or optional configuration for the interface.


### Additional attributes:

Note that some field definitions are still missing, specifically for:

`authentication`        | Object   | The authentication configuration for accessing the resource.
`network_interfaces`    | List     | A list of network interfaces available for the resource. These will be referenced by Strigo interfaces.

These will be elaborated on later.


### Response Structure:

Note that Strigo will convey the success or failure of webhook calls based on standard HTTP response codes (that the backend should provide).


## Example Message

All webhook messages should look like the following example.

The differences between them will be the `message_id`, `type`, `action` and `entity_ids` provided.

For a list of possible `type`s and `action`s, see below.


> Creation Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/webhooks/events/incoming" \
    -d @- <<EOF
    {
        source_message_id: "dfede374",
        type: "RESOURCE",
        action: "CREATED",
        timestamp: "2020-10-05T08:39:09+00:00",
        data: {
            resources: [
                {
                    id: "25f377ac",
                    type: "VM",
                    status: "STARTING",
                    name: "server",
                    config: {
                        network_interface: {
                            public_ip: "32.17.144.2",
                            private_ip: "10.0.0.6",
                            dns: "5108e970-labs.mycompany.com"
                        }
                    }
                },
                {
                    id: "56ea830e",
                    type: "VM",
                    status: "STARTING",
                    name: "agent",
                    config: {
                        network_interface: {
                            public_ip: "32.17.144.3",
                            private_ip: "10.0.0.8"
                        }
                    }
                },
                {
                    id: "619a8bbe",
                    type: "VM",
                    status: "STARTING",
                    name: "client",
                    config: {
                        network_interface: {
                            public_ip: "32.17.149.7",
                            private_ip: "10.0.0.9"
                        }
                    }
                },
                {
                    id: "acf1109b",
                    type: "URL",
                    status: "READY",
                    name: "hosted_application",
                    config: {
                        address: "https://my.webpage.com:3131"
                    }
                }
            ],
            interfaces: [
                {
                    name: "Server"
                    type: "TERMINAL",
                    region: "us-east-1",
                    resource_id: "25f377ac"
                },
                {
                    name: "Server Web Application"
                    type: "WEB_PAGE",
                    region: "us-east-1",
                    resource_id: "25f377ac",
                    config: {
                        port: 8080
                    }
                },
                {
                    name: "Agent"
                    type: "TERMINAL",
                    region: "us-east-1",
                    resource_id: "56ea830e",
                    config: {
                        port: 2022,
                        authentication: {
                            type: "keypair",
                            data: {
                                key: "..."
                            }
                        }
                    }
                },
                {
                    name: "Client"
                    type: "DESKTOP",
                    region: "us-east-1",
                    resource_id: "619a8bbe",
                    config: {
                        port: "3389",
                        authentication: {
                            type: "generated_username_password",
                            data: {
                                username: "Administrator",
                                password: "p@$$w0rd"
                            }
                        }
                    }
                },
                {
                    name: "Hosted Service"
                    type: "WEB_PAGE",
                    region: "eu-north-1",
                    resource_id: "acf1109b"
                }
            ]
        }
    }
EOF
```


## Available types, statuses, resources and interfaces.

The following represents an exhaustive list of resource types and actions, and interface types.

### Actions

* `CREATED` => Resources were created.
* `UPDATED` => Resources were updated.
* `DELETED` => Resources were deleted.

### Resource types

* `VM` => Refers to a virtual machine.
* `URL` => Refers to a public/WEB_PAGE URL.

### Resource statuses

* `STARTING`
* `PREPARING`
* `READY`
* `STOPPING`
* `STOPPED`
* `DELETING`
* `DELETED`
* `ERROR`

### Interface types

* `TERMINAL` => An SSH-based shell.
* `DESKTOP` => A desktop interface to either a Linux or Windows based machine, via RDP.
* `WEB_PAGE` => An iframe that redirects to either a web server hosted on a VM, or an external website.
