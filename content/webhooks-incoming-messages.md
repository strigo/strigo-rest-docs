---
weight: 1010
---


# Webhooks - Incoming Messages

## Incoming Message

The following messages are sent from the customer's backend to Strigo, where Strigo can then perform any required actions.

For example, once the customer's backend has created a lab for a student, Strigo can use the information from the incoming message to display a terminal interface.

See [Outgoing Messages](#webhooks-outgoing-messages) for examples on the webhook messages Strigo sends.

### Attributes:

Attribute               | Type     | Description
---------               | -------  | -------
`source_message_id`     | String   | The source message's unique identifier. This is the `message_id` provided in the webhook.
`type`                  | String   | The type of resource Strigo needs to handle.
`status`                | String   | The current state of the resource (CRUD?).
`data`                  | Object   | An object containing `resources` and `interfaces` lists.

### Response Structure:

Note that Strigo will convey the success or failure of webhook calls based on standard HTTP response codes (that the backend should provide).


## Example Message

All webhook messages should look like the following example.

The differences between them will be the `message_id`, `type`, `action` and `entity_ids` provided.

For a list of possible `type`s and `action`s, see below.


> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_BACKEND_USER}:${ORG_BACKEND_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://training.mycompany.com/webhooks/events" \
    -d @- <<EOF
    {
        "source_message_id": "4dd6be9e",
        "type": "RESOURCE",
        "status": "CREATED",
        "timestamp": "2020-09-27T19:00:00.000+00:00",
        "data": {
            "resources": [
                {
                    "id": "5108e970",
                    "fields": {
                        "added": [
                                // Add an item to an array.
                                {
                                    "path": "connectivity_info",
                                    "value": {
                                        "id": "17d10840",
                                        "private_ip": "172.31.10.4"
                                    }
                                }
                        ],
                        "updated": [
                            // Update an item in an array.
                            {
                                "path": "connectivity_info.0.public_ip",
                                "value": "142.94.13.6"
                            },
                            // Update an object.
                            {
                                "path": "status",
                                "value": "ready"
                            }
                        ]
                    }
                }
            ],
            "interfaces": [
                {
                    "id": "25f377ac",
                    "name": "CLIENT",
                    "type": "TERMINAL",
                    "resource_id": "5108e970",
                    "data": {
                        "connectivity_info": {
                            "id": "e9c09fc2",
                            "port": "22"
                        },
                        "credentials": {
                            "type": "generated_username_password",
                            "data": {
                                "username": "admin",
                                "password": "p@$$w0rd"
                            }
                        }
                    }
                }
            ]
        }
    }
EOF
```

## Available types, statuses, resources and interfaces.
