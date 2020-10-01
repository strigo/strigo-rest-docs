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
        source_message_id: "dfede374",
        type: "RESOURCE",
        action: "CREATED",
        data: {
            resources: [
                {
                    id: "25f377ac",
                    type: "VM",
                    name: "server",
                    data: {
                        status: "LAUNCHING"
                    }
                },
                {
                    id: "56ea830e",
                    type: "VM",
                    name: "agent",
                    data: {
                        status: "LAUNCHING"
                    }
                },
                {
                    id: "619a8bbe",
                    type: "VM",
                    name: "client",
                    data: {
                        status: "LAUNCHING"
                    }
                }
            ],
            interfaces: [
                {
                    type: "TERMINAL",
                    resource_id: "25f377ac",
                    ...
                },
                {
                    type: "TERMINAL",
                    resource_id: "619a8bbe",
                    ...
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
* `URL` => Refers to a public/webview URL.

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

* `TERMINAL`
* `WEB_INTERFACE`
* `REMOTE_DESKTOP`
